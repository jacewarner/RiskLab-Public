# Changelog

## v1.1.3 - January 19, 2026
- Added GitHub App workflow to sync README.md and CHANGELOG.md to the public repo on every push.
- Scoped GitHub App token to the public repo so sync pushes authenticate correctly.
- Refocused README on product coverage and moved build/deploy instructions to BUILD.md.
- Expanded FX snapshot with strategy coverage and complex calculation callouts.
- Expanded README coverage details for Markets, Risk, Options, Hedging, and calculators.
- Added FX subpages covering forwards/swaps, carry/funding, volatility, and options structures.
- Expanded README with deeper section detail and positioning around model clarity and stress analysis.

---

## v1.1.2 - January 16, 2026
- Added Quadratic VaR overview and calculator using delta-gamma with Cornish-Fisher percentiles and EWMA decay.

---

## v1.1.1 - December 11, 2025
- CI/publish: temporarily build/push amd64 images only (arm64 under QEMU hit illegal-instruction during npm build); re-enable arm64 when a native builder is available or base image is adjusted.
- CI docker-build job now forces linux/amd64 to avoid arm64 QEMU failures during release checks.
- Consolidated Docker Compose services into a single `risklab` service and simplified Makefile targets.
- Removed `Dockerfile.dev` after consolidating on the production Docker build.
- Updated `baseline-browser-mapping` dev dependency to refresh browser support data.
- Ran `npm audit fix` to resolve dependency vulnerabilities after the update.
- Added GMaR section with overview and calculator between VaR and Options in the Risk sidebar.
- Added Delta Hedging overview page with intro, formulas, and practical notes.
- Added Delta Hedge calculator page and interactive calculator for hedge sizing.
- Added CAT bond section under Fixed Income covering triggers, diversification, and a Jamaica hurricane example.
- Added Fixed Income calculator for bond pricing, Macaulay/modified duration, and DV01.
- Restructured Fixed Income: added Bonds category with calculator and CAT bond page nested under Fixed Income.
- Added Treasury Bills page and calculator under Fixed Income → Bonds, including laddering notes.

---

## v1.1.0 - December 10, 2025
- Added Markets section above Risk to collect asset-class specifics.
- Added Markets overview plus snapshots for Equities, Commodity Trading, FX, and Fixed Income with key drivers and risk checks.
- Added Energy Products sub-section with pages for power, natural gas, crude, and environmental products, covering physical and financial trading aspects.
- Nested Energy Products under Commodity Trading in the Markets navigation.
- Added dedicated Power Physical vs Financial page detailing DA/RT, capacity ICAP/UCAP, ancillaries, PPAs, transmission, and CRR/FTR obligations alongside financial overlays.
- Expanded Power Physical vs Financial with a generation entry covering dispatch economics, tolling, and heat-rate style deals.
- Added Natural Gas Physical vs Financial subpage with GDD/IF/NYMEX LD1 and financial hedges (HH futures, basis swaps, options, strips), nested under Natural Gas.
- Added Natural Gas Storage page with WACOG explainer and calculator for injection costs plus carry.
- Expanded Natural Gas Storage with PAL (park/loan) overview and hedging notes.
- Added Power Storage / Battery page covering emerging battery/VPP participation, services (energy arb, ancillaries, capacity, demand response), and practical considerations.
- Navbar now has direct Markets and Risk links (plus Docs) to expand the relevant sidebar section.
- Navbar now only shows Markets and Risk; sidebar auto-collapses categories when switching sections.
- Corrected PAL hedging guidance (park = short futures on return gas; loan = long futures on owed gas).
- Added Quanto Option doc and calculator covering usage, quanto drift adjustment, and Black-style pricing under Options.

---

## v1.0.6 - December 10, 2025
- Added Beta Hedge overview covering purpose, who uses it, and practical considerations (fit, basis risk, lookbacks).
- Added Beta Hedge calculator to estimate beta from paired returns and size futures hedge contracts with signed outputs.
- Linked the Beta Hedge pages under a new Hedging / Factor Hedging section after Options.

---

## v1.0.5 - December 10, 2025
- Added VaR & Expected Shortfall section with primers on usage, lookbacks, scaling, and tail risk.
- Added interactive VaR/ES calculator page combining parametric (normal) and historical methods with horizon/notional scaling.
- Linked the new VaR pages in the Risk sidebar beneath Correlations.
- Added Correlations section (overview page) under Risk navigation.
- Added correlation calculator (paired sample correlation/covariance with summary stats).

---

## v1.0.4 - December 7, 2025
- Implied vol solver now returns σ=0 when the market price equals discounted intrinsic value instead of reporting no bracket.
- Navbar version badge now shows branch + commit date (drops package version).
- Added “Volatility 101” primer covering what volatility is, why it matters, and how traders view skews/smiles.
- Added illustrative volatility skew image to Volatility 101.
- Fixed the skew illustration axis label so the full “Implied Volatility” text renders.
- Moved volatility docs under /docs/volatility (Volatility 101, Historical, Implied) and updated links/sidebar.

---

## v1.0.3 - December 6, 2025
- Move Volatility out of Options into its own Risk-level sidebar category above Options.
- Add volatility reference pages for historical and implied volatility with formulas, solver guidance, and sidebar/index links.
- Add interactive historical volatility calculator that parses prices or log returns and annualizes sample stdev.
- Add implied volatility solver (Black–76, bisection with intrinsic bound checks and expanding bracket).
- Implied vol calculator inputs now span full column width for consistent layout.


---

## v1.0.2
- Publish workflow now runs a fast amd64-only build (no push) on PRs and keeps multi-arch push only on branch/tag pushes, both cached.
- Publish workflow logs plain buildx progress for multi-arch builds to ease debugging of slow/failing steps.
- Turnbull-Wakeman calculator lets you choose calendar vs business-day basis for expiry/averaging.
- Turnbull-Wakeman calculator adds US/UK holiday-aware business-day options (assumes ~252/253 trading days per year).
- Turnbull-Wakeman pricing now uses the averaging horizon in the d1/d2 volatility term to better align with reference implementations.
- Reworked Turnbull-Wakeman to follow the cited futures-Asian formulation: zero cost-of-carry, explicit M-based sigma_A, optional strike scaling when averaging has begun, and Black-76 on the synthetic average.
- Updated TW mapping to follow explicit T_total/T2/τ guidance and strike adjustment from the provided breakdown; M1/M2 now use the clarified inputs.
- TW calculator now matches the provided Excel sheet formulas for M1/M2, sigma_A, b, strike adjustment, and pricing over the remaining averaging window.
- Fixed TW d₁/d₂ to be based on the moment-matched average (M1) with proper discounting, eliminating the huge positive/negative outputs and aligning with the Excel walkthrough.
- TW strike leg is now discounted only over the remaining averaging horizon (T_avg), matching the spreadsheet and lifting the call price to the expected ~0.215 in the provided scenario.
- Restored the TW calculator discount output (used in the UI) after the strike-leg discount change so the component renders correctly post-rebuild.
- Days to expiry now feeds the averaging horizon when adjustments are off and introduces an extra settlement discount from the last fixing to maturity, so expiry changes affect the APO price/theta even when the averaging window finishes earlier.

---

## v1.0.1

- Add Dockerfile and Dockerfile.dev for dev/prod container workflows with configurable host/port and Cloudflare tunnel guidance.
- Add docker-compose.yml with dev/prod services (default host port 8090) plus README updates for port selection.
- Replace navbar GitHub link with version badge showing dev/v1.0.1 (2025-11-17).
- Version badge now auto-populates from git branch/commit date (env overrides) so dev/prod builds display their own branch/version/date.
- Add Makefile shortcuts (`make build-dev`, `make build-prod`) that wrap the compose dev/prod services with default PORT=8090.
- Add CODEOWNERS assigning all paths to @keatre.
- Add CI workflow to npm ci, typecheck, and build on pushes/PRs.
- Add publish-image workflow to build and push multi-arch Docker images to GHCR.
- Adjust compose Cloudflare tunnel to log to ./logs/risklab.log and start with make targets (cloudflare profile enabled).
- Add log wrapper + compose hooks to write dev/prod/tunnel output to /logs/risklab.log with size/days retention envs (defaults: 2MB, 7 days).
- Add TZ defaults and tzdata to images; log rotation respects TZ and can be overridden via .env.
- Simplified cloudflared logging to reuse shared log wrapper (fix compose command parsing).
- Fix log wrapper syntax so dev/prod/tunnel containers start cleanly with rotation.
- Add dedicated cloudflared image (alpine + tzdata + log wrapper) to restore shell availability and keep logging/rotation working.
- Switch cloudflared entrypoint to /bin/ash + log wrapper to avoid missing /bin/sh runtime failures.
- Add timestamping to log wrapper output and pin app port to 3000 inside containers while mapping host PORT (default 8090).
- Install git in Dockerfile.dev for version badge and dev tooling.
- Makefile: build-dev/build-prod no longer start cloudflared; new build-cloudflare target to launch tunnel separately.
- Default Docusaurus to dark mode for all users.
- Makefile runs dev/prod/cloudflared in detached mode to avoid terminal blocking on startup.
- Add git to runtime image (Dockerfile) to eliminate version badge git-not-found warnings.
- Makefile build-cloudflare now cleans orphans and force-recreates the tunnel to avoid stale network errors.
- Makefile build-cloudflare no longer stops other services; it just recreates cloudflared without dependencies.
- Compose now pre-trusts /app as a safe git directory to silence ownership warnings and enable the version badge.
- Footer links and titles centered for consistent alignment.
- Install git in Dockerfile build stage so version badge works during prod builds.
- Compose commands now export VERSION_BRANCH/VERSION/VERSION_DATE from git (tag/date fallback) before start/serve to ensure the navbar badge populates.
- Log wrapper now sets VERSION_BRANCH/VERSION/VERSION_DATE from git/tag/package at startup (and trusts /app) so the navbar badge can populate without manual envs; compose commands reverted to leaner start.
- Navbar version badge now forces safe git config via `git -c safe.directory=/app` when resolving branch/date to avoid ownership warnings.
- Version badge hides duplicate version when branch already includes the tag.
- Version badge now strips leading 'v' and skips showing version if branch already contains it.
- Version badge now detects version-like suffixes on the branch (e.g., /v1.0.1) and omits appending the version to avoid duplicates.
- Version badge detection loosened to any version-like token in branch (no suffix requirement) to prevent duplicate version text.
- Version badge now collapses any repeated version token in the display string to ensure it renders only once.
- Simplified version badge logic: if branch version matches, show branch only; otherwise append version once.
- Add npm lint alias to typecheck and run it in CI; CI now also builds the Docker image (no push) to catch Dockerfile regressions.
- Release Drafter workflow now only runs on main to avoid PR failures until config is on the default branch.
- Log wrapper now uses pipefail and returns the wrapped command's exit code so failures surface correctly.
- Optimize Docker builds: enable npm cache mounts in Dockerfiles, use BuildKit cache in publish image workflow, and add a 30-minute timeout/skip on PRs for the docker CI job.
