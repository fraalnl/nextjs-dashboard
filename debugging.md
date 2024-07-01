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
### Creating DB
```
PS D:\Develop\NextJS\nextjs-dashboard> pnpm i @vercel/postgres
 WARN  Unsupported engine: wanted: {"node":">=20.12.0"} (current: {"node":"v20.10.0","pnpm":"9.4.0"})
 WARN  6 deprecated subdependencies found: are-we-there-yet@2.0.0, gauge@3.0.2, glob@7.2.3, inflight@1.0.6, npmlog@5.0.1, rimraf@3.0.2
Packages: +223
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 ERR_PNPM_EPERM  EPERM: operation not permitted, unlink 'D:\Develop\NextJS\nextjs-dashboard\node_modules\.pnpm\bufferutil@4.0.8\node_modules\bufferutil\prebuilds\win32-x64\node.napi.node'
Progress: resolved 251, reused 223, downloaded 1, added 3
```
- solution: install latest LTS node.js (as if it were the first time you install it, no need to uninstall the old one), terminal run as admin, restart the project

install db `pnpm i @vercel/postgres` 
- Tip: use multiple tags of terminal(admin) to run the project and install db respectively