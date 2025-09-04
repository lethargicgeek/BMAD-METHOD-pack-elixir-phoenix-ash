# Architecture Design Changes

## Story Reference
[NNNNNN-StoryName]

## Architecture Overview
[High-level architecture description]

## Ash Resources

### Resource: [ResourceName]
```elixir
defmodule MyApp.ResourceContext.ResourceName do
  use Ash.Resource,
    data_layer: AshPostgres.DataLayer

  attributes do
    # UUID primary key
    uuid_primary_key :id
    
    # Attributes
    attribute :name, :string, allow_nil?: false
    attribute :status, :atom, constraints: [one_of: [:active, :inactive]]
    
    # Timestamps
    timestamps()
  end

  relationships do
    belongs_to :user, MyApp.Accounts.User
    has_many :items, MyApp.ResourceContext.Item
  end

  actions do
    defaults [:create, :read, :update, :destroy]
    
    # Custom actions
    action :custom_action, :type do
      # Implementation
    end
  end

  policies do
    policy action_type(:read) do
      authorize_if expr(public == true)
    end
  end
end
```

## Phoenix Contexts

### Context Module: [ContextName]
```elixir
defmodule MyAppWeb.ContextName do
  # Context implementation
end
```

## LiveView Components

### Component: [ComponentName]
```elixir
defmodule MyAppWeb.Live.ComponentName do
  use MyAppWeb, :live_view
  
  # LiveView implementation
end
```

## Database Schema

### Table: [table_name]
```sql
CREATE TABLE table_name (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  -- columns
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

## API Design

### REST Endpoints
- `GET /api/resources` - List resources
- `GET /api/resources/:id` - Get resource
- `POST /api/resources` - Create resource
- `PUT /api/resources/:id` - Update resource
- `DELETE /api/resources/:id` - Delete resource

### GraphQL Schema
```graphql
type Resource {
  id: ID!
  name: String!
  # fields
}
```

## Security Considerations
- Authentication method
- Authorization policies
- Data validation rules
- Rate limiting

## Performance Considerations
- Query optimization
- Caching strategy
- Background jobs
- Real-time updates