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