# AGENTS.md

## Critical: Stale Documentation

- **CLAUDE.md is out of date.** It lists program ID `GPfsmgJRLLxaWScL2PPEt5TAgAjzNYTaMuzmsPipnfSv` but the actual deployed program ID is `CXA848KGbmaYExskMu2XaxEwVpPh3G8z2776N4GdGif1` (confirmed in `anchor/Anchor.toml:9` and `anchor/programs/auction/src/lib.rs:8`). Always verify program IDs from these files, not CLAUDE.md.
- **anchor/README.md is a generic vault template.** It describes a "vault" program, not the actual auction program. Do not follow it.

## Verified Commands

```bash
pnpm run dev          # Next.js dev (turbopack, preferred)
pnpm run dev:webpack  # webpack fallback

pnpm run lint         # ESLint
pnpm run format       # Prettier write
pnpm run format:check # Prettier check
pnpm run ci           # build + lint + format:check

pnpm run anchor-build # Build anchor program only
pnpm run codama:js   # Generate TS client from IDL → app/generated/auction/
pnpm run setup        # anchor-build && codama:js (full contract + client update)
pnpm run anchor-test  # Run anchor tests (no deploy)
```

**Order matters for contract changes:** `pnpm run setup` (or manual: `anchor build` from anchor dir, then `pnpm run codama:js`).

## Architecture

- **Frontend**: Next.js 16 (App Router) at `/`. Route groups: `(dashboard)/organizer`, `(dashboard)/user`, `/login/*`.
- **Smart contract**: Anchor program `auction` at `anchor/programs/auction/`. Deployed on devnet at `CXA848KGbmaYExskMu2XaxEwVpPh3G8z2776N4GdGif1`.
- **Wallet**: Dynamic Labs SDK (`@dynamic-labs/sdk-react-core` + `@dynamic-labs/solana`).
- **Candy Machine**: Metaplex UMI for ticket minting (`lib/solana/candy-machine.ts`).
- **Codama client**: Generated to `app/generated/auction/` from `anchor/target/idl/auction.json`.
- **ESLint ignores**: `app/generated/**` (codama output) and `.next/**`.

## Environment Setup

```bash
cp .env.example .env.local
```

Required vars: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`, `NEXT_PUBLIC_DYNAMIC_ENVIRONMENT_ID`, `NEXT_PUBLIC_SOLANA_RPC_URL` (defaults to devnet).

## Deployment (if program changes)

1. `solana-keygen new -o anchor/target/deploy/auction-keypair.json`
2. `solana address -k anchor/target/deploy/auction-keypair.json`
3. Update `anchor/Anchor.toml` `[programs.devnet]` and `anchor/programs/auction/src/lib.rs` `declare_id!()` with new ID
4. `cd anchor && anchor build && anchor deploy --provider.cluster devnet`
5. `pnpm run codama:js`

## Prettier

`semi: true`, `singleQuote: false`, `tabWidth: 2`, `trailingComma: "es5"` (from `.prettierrc`).