# HOC vs. Render Props

https://github.com/apollographql/apollo-client/issues/3253

https://www.apollographql.com/docs/react/api/react-apollo

https://www.apollographql.com/docs/react/api/react-apollo#graphql

graphql(query, [config])(component)

The graphql() function is the most important thing exported by react-apollo. With this function you can create higher-order components that can execute queries and update reactively based on the data in your Apollo store. The graphql() function returns a function which will “enhance” any component with reactive GraphQL capabilities. This follows the React higher-order component pattern which is also used by react-redux’s connect function.

# Cache

https://www.npmjs.com/package/apollo-cache-inmemory

https://www.apollographql.com/docs/react/advanced/caching

# Mutations

https://github.com/graphql/graphiql/issues/72

https://www.apollographql.com/docs/react/essentials/local-state

```
import { ApolloClient } from 'apollo-client';
import { InMemoryCache } from 'apollo-cache-inmemory';

const client = new ApolloClient({
  cache: new InMemoryCache(),
  resolvers: {
    Mutation: {
      toggleTodo: (_root, variables, { cache, getCacheKey }) => {
        const id = getCacheKey({ __typename: 'TodoItem', id: variables.id })
        const fragment = gql`
          fragment completeTodo on TodoItem {
            completed
          }
        `;
        const todo = cache.readFragment({ fragment, id });
        const data = { ...todo, completed: !todo.completed };
        cache.writeData({ id, data });
        return null;
      },
    },
  },
});
```

# Queries

https://www.apollographql.com/docs/react/essentials/queries#basic

https://graphql.org/learn/queries/#fragments


First, let's create our GraphQL query. Remember to wrap your query string in the gql function in order to parse it into a query document.

# Local State Management

https://www.apollographql.com/docs/react/essentials/local-state

# React Hooks

https://github.com/apollographql/react-apollo/pull/2892

# Fragments

https://www.apollographql.com/docs/react/advanced/fragments

A GraphQL fragment is a shared piece of query logic.

```

fragment NameParts on Person {
  firstName
  lastName
}

query GetPerson {
  people(id: "7") {
    ...NameParts
    avatar(size: LARGE)
  }
}
```

It's important to note that the component after the on clause is designated for the type we are selecting from. In this case, people is of type Person and we want to select the firstName and lastName fields from people(id: "7").

There are two principal uses for fragments in Apollo:

Sharing fields between multiple queries, mutations or subscriptions.
Breaking your queries up to allow you to co-locate field access with the places they are used.


https://medium.com/open-graphql/fragment-driven-uis-with-apollo-17d933fa1cbe


https://medium.com/graphql-mastery/graphql-fragments-and-how-to-use-them-8ee30b44f59e

Each fragment contains the name of the fragment (userFields), to what type we are applying this fragment (User) and the selection set (id, firstName, lastName, phone and username).

Now we can rewrite the getUsers query with the fragment and spread operator.

```
query getUsers {
  admins: users(role: admin) {
    ...userFields
  }
  accountants: users(role: accountant) {
    ...userFields
  }
}

fragment userFields on User {
   id
   firstName
   lastName
   phone
   username
}

```

https://spectrum.chat/graphql/general/apollo-how-to-reuse-fragments-that-are-in-another-file~839f6551-2492-44c3-976e-16d263ea1a3b

# Import .graphql files

https://github.com/apollographql/apollo-link-state/issues/283

# Apollo Client vs. Redux

https://codeburst.io/graphql-and-apollo-client-by-example-part-5-2eb206f3aff5

tore (Redux) / Cache (Apollo Client)

Action Creators (Redux) / Mutations in typeDef.ts (Apollo Client)

Reducers (Redux) / Mutations in resolvers.ts (Apollo Client)

Selectors (Redux) / Queries in typeDefs.js (Apollo Client)

