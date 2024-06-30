### When deploying on Vercel
```
Failed to compile.
./app/ui/customers/table.tsx:2:10
Type error: Module '"@/app/ui/fonts"' has no exported member 'lusitana'.
  1 | import Image from 'next/image';
> 2 | import { lusitana } from '@/app/ui/fonts';
```
Because my vscode can't recognize the font Lusitana, and I skipped it.
- solution: change `lusitana` into `inter`, a recognizable font

Locally compiled successfully. Yet, still failed to compile on Vercel. Strangely, the Vercel log still points to the line which I've changed, though with the latest commit message from github.

In fact, by finding `ctrl+shift+F` and select `open in editor`, I found more occurrences of `lusitana` throughout the project.
Replaced them all with `inter`, will push, redeploy.