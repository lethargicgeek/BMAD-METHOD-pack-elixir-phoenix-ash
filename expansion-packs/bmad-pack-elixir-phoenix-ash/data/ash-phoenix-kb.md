# Ash Phoenix Knowledge Base

## Ash Framework Essentials

### Core Concepts
- **Resources**: Central data models with built-in CRUD operations
- **Actions**: Operations that can be performed on resources
- **Attributes**: Fields on resources with types and constraints
- **Relationships**: Connections between resources
- **Calculations**: Derived values computed from resource data
- **Aggregates**: Computed values across relationships
- **Policies**: Authorization rules for resources and actions

### Resource Definition Pattern
```elixir
defmodule MyApp.Context.Resource do
  use Ash.Resource,
    data_layer: AshPostgres.DataLayer

  postgres do
    table "resources"
    repo MyApp.Repo
  end

  attributes do
    uuid_primary_key :id
    attribute :name, :string, allow_nil?: false
    timestamps()
  end

  actions do
    defaults [:create, :read, :update, :destroy]
  end

  policies do
    policy action_type(:read) do
      authorize_if expr(public == true)
    end
  end
end
```

## Phoenix LiveView Patterns

### Basic LiveView Structure
```elixir
defmodule MyAppWeb.ResourceLive.Index do
  use MyAppWeb, :live_view
  
  @impl true
  def mount(_params, _session, socket) do
    {:ok, assign(socket, :resources, list_resources())}
  end
  
  @impl true
  def handle_event("delete", %{"id" => id}, socket) do
    # Handle deletion
    {:noreply, socket}
  end
end
```

### LiveView with Ash Integration
```elixir
def list_resources do
  MyApp.Context.Resource
  |> Ash.Query.for_read(:read)
  |> MyApp.Api.read!()
end

def create_resource(params) do
  MyApp.Context.Resource
  |> Ash.Changeset.for_create(:create, params)
  |> MyApp.Api.create()
end
```

## Common Patterns

### Multi-tenancy
```elixir
multitenancy do
  strategy :context
  attribute :tenant_id
end
```

### Soft Deletes
```elixir
actions do
  destroy :destroy do
    soft? true
  end
end
```

### Pagination
```elixir
actions do
  read :read do
    pagination offset?: true, default_limit: 20
  end
end
```

### File Uploads with Arc
```elixir
attribute :avatar, :string

calculations do
  calculate :avatar_url, :string, fn records, _ ->
    Enum.map(records, fn record ->
      MyApp.Avatar.url({record.avatar, record})
    end)
  end
end
```

## Testing Strategies

### Resource Testing
```elixir
describe "create/1" do
  test "creates resource with valid data" do
    assert {:ok, resource} = 
      MyApp.Context.Resource
      |> Ash.Changeset.for_create(:create, %{name: "Test"})
      |> MyApp.Api.create()
    
    assert resource.name == "Test"
  end
end
```

### LiveView Testing
```elixir
test "displays resources", %{conn: conn} do
  resource = resource_fixture()
  {:ok, view, html} = live(conn, ~p"/resources")
  
  assert html =~ resource.name
end
```

## Performance Optimization

### Query Loading
```elixir
MyApp.Context.Resource
|> Ash.Query.load([:relationship, :calculation])
|> MyApp.Api.read!()
```

### Batch Loading
```elixir
actions do
  read :read do
    prepare build(load: [:items_count])
  end
end
```

### Async Operations
```elixir
Task.async_stream(resources, fn resource ->
  process_resource(resource)
end, max_concurrency: 10)
```

## Common Integrations

### Authentication (Pow/Guardian)
```elixir
policies do
  policy action_type(:all) do
    authorize_if expr(^actor(:id) == user_id)
  end
end
```

### Background Jobs (Oban)
```elixir
changes do
  change after_action(fn changeset, record ->
    %{resource_id: record.id}
    |> MyApp.Workers.ProcessResource.new()
    |> Oban.insert()
    
    {:ok, record}
  end)
end
```

### GraphQL (Absinthe)
```elixir
graphql do
  type :resource
  
  queries do
    get :get_resource, :read
    list :list_resources, :read
  end
  
  mutations do
    create :create_resource, :create
    update :update_resource, :update
    destroy :destroy_resource, :destroy
  end
end
```

## Error Handling

### Custom Errors
```elixir
defmodule MyApp.Errors.CustomError do
  use Ash.Error.Exception
  
  def message(%{field: field}) do
    "Invalid value for #{field}"
  end
end
```

### Error Recovery
```elixir
case MyApp.Api.create(changeset) do
  {:ok, resource} -> 
    {:ok, resource}
  {:error, %Ash.Error.Invalid{} = error} ->
    handle_validation_error(error)
  {:error, error} ->
    handle_generic_error(error)
end
```

## Best Practices

1. **Use Contexts**: Organize resources into logical contexts
2. **Define Clear Actions**: Be explicit about what operations are allowed
3. **Implement Policies Early**: Add authorization from the start
4. **Test at Multiple Levels**: Unit, integration, and acceptance tests
5. **Use Calculations**: Avoid N+1 queries with proper loading
6. **Handle Errors Gracefully**: Provide meaningful error messages
7. **Document APIs**: Use OpenAPI specifications for REST APIs
8. **Monitor Performance**: Use telemetry and metrics
9. **Version APIs**: Plan for backward compatibility
10. **Secure by Default**: Always validate and authorize