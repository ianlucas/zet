# How I Structure TypeScript and React Projects

Currently, I am working on two main personal projects using TypeScript and React. One is a Progressive Web App intended for personal trainers, and the other is a custom matchmaking service for a first-person shooter game. My tech stack includes TypeScript, Prisma, tRPC, and React. I believe tRPC is the most crucial component because it eliminates the need to worry about HTTP routes and makes data fetching a breeze. I'm not using Next.js because my apps have some specific requirements, so the structure I am about to show may not be applicable for applications using Next.js or other major frameworks. (By the way, you should consider using the T3 Stack for that.)

## Folder structure

So here's the folder structure I've settled in.

```
./client                # Created with Vite.
./client/src/hooks      # Store React hooks. Each file is the name of the hook, e.g. useIsVisible.ts.
./client/src/icons      # React SVG icons components. Each file is the name of the component, e.g. ClipboardIcon.ts.
./client/src/lib        # Supporting libraries for the client. Each file is a module with misc utils, e.g. trpc.ts.
./client/src/store      # Store Jotai (or similar) atoms. For simple projects, a simple app.ts is enough.
./client/src            # React components.
./prisma                # Created with Prisma.
./server/lib            # Supporting libraries for the server. Each file is a module with misc utils, e.g. regex.ts.
./server/main.ts        # Instantiate Express and integrate with tRPC.
./server/trpc.ts        # Define all tRPCs components like context and procedures.
```