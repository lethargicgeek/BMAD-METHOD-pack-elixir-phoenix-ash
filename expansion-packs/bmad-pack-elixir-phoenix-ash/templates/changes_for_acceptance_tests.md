# Acceptance Tests Changes

## Story Reference
[NNNNNN-StoryName]

## Test Overview
[Brief description of test strategy]

## Acceptance Criteria Tests

### Criterion 1: [Description]
```elixir
test "criterion_1_description", %{conn: conn} do
  # Test implementation
end
```

### Criterion 2: [Description]
```elixir
test "criterion_2_description", %{conn: conn} do
  # Test implementation
end
```

## Test Categories

### Unit Tests

#### Resource Tests
```elixir
defmodule MyApp.ResourceTest do
  use MyApp.DataCase
  
  describe "resource actions" do
    test "create with valid data" do
      # Test implementation
    end
    
    test "create with invalid data" do
      # Test implementation
    end
  end
end
```

### Integration Tests

#### Context Tests
```elixir
defmodule MyApp.ContextTest do
  use MyApp.DataCase
  
  describe "context functions" do
    test "list_resources/0" do
      # Test implementation
    end
  end
end
```

### LiveView Tests

```elixir
defmodule MyAppWeb.FeatureLiveTest do
  use MyAppWeb.ConnCase
  import Phoenix.LiveViewTest
  
  describe "Index" do
    test "lists all resources", %{conn: conn} do
      {:ok, _index_live, html} = live(conn, ~p"/resources")
      assert html =~ "Resources"
    end
  end
end
```

### API Tests

```elixir
defmodule MyAppWeb.ResourceControllerTest do
  use MyAppWeb.ConnCase
  
  describe "index" do
    test "lists all resources", %{conn: conn} do
      conn = get(conn, ~p"/api/resources")
      assert json_response(conn, 200)["data"] == []
    end
  end
end
```

## Test Data Setup

### Factories
```elixir
defmodule MyApp.Factory do
  use ExMachina.Ecto, repo: MyApp.Repo
  
  def resource_factory do
    %MyApp.Resource{
      name: sequence(:name, &"Resource #{&1}"),
      status: :active
    }
  end
end
```

### Fixtures
```elixir
def resource_fixture(attrs \\ %{}) do
  {:ok, resource} =
    attrs
    |> Enum.into(%{name: "Test Resource"})
    |> MyApp.Context.create_resource()
  
  resource
end
```

## Test Scenarios

### Happy Path
1. User can create resource
2. User can view resource
3. User can update resource
4. User can delete resource

### Edge Cases
1. Invalid data handling
2. Authorization failures
3. Concurrent updates
4. Rate limiting

### Error Scenarios
1. Network failures
2. Database constraints
3. Invalid state transitions
4. Missing required fields

## Performance Tests

```elixir
test "handles large datasets efficiently" do
  # Create 1000 resources
  # Measure query time
  # Assert performance threshold
end
```

## Security Tests

```elixir
test "prevents unauthorized access" do
  # Test authorization policies
end

test "sanitizes user input" do
  # Test input validation
end
```

## Test Coverage Goals
- Line Coverage: >= 80%
- Branch Coverage: >= 75%
- Critical Path Coverage: 100%

## Manual Test Checklist
- [ ] UI displays correctly
- [ ] Forms validate properly
- [ ] Error messages are clear
- [ ] Performance is acceptable
- [ ] Accessibility requirements met