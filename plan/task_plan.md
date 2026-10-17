# Task plan — Protocolized Inspire

Goal: a sibling of `../mth-inspire` for **protocol art**: works where an artist / designer authors a protocol,
the protocol shapes what a group of people does, and that group behaviour is the work.
Examples named by the user: Pak, terra0, Sol LeWitt; most recent works are smart-contract based.

## Decisions
- Same architecture as mth-inspire: `data/raw/*.json` batches → `tools/build_data.py` → `data/entries.js` + static site.
- Replace `organisms` with `mechanisms` (1–3 protocol primitives) and add `substrate` (paper, body, post, internet, ethereum…).
- Replace `method` with two protocol fields: `protocol` (the rules) and `collective` (what the group did).
- Replace the Papers view with a Timeline view (the lineage from 1920s instructions to smart contracts).
- Local only: no git remote, no publish, no domain until the user decides. Placeholder site URL `https://protocolized.reality.design`.

## Phases
- [x] P0 Scaffold: taxonomy, SCHEMA, RESEARCH_BRIEF, tools, site, README, /add-work command (empty build OK, JS/py syntax OK)
- [ ] P0 Research batches (8 parallel agents): score, social, network, onchain-pak, onchain-rules, onchain-coauthor, autonomous, theory
- [ ] P0 Validate + build + fix dropped media
- [ ] P1 Local preview check (`./serve.sh`, port 8933)
- [x] P2 git init, remote, domain — user chose repo realitydeslab/protocolized-inspire (public, like mth; renamed to realitydeslab/protocolized-reality-inspire on user request, then on 2026-10-17 to realitydeslab/protocolized-reality-inspires to match the local folder; domain unchanged) and domain protocolized.reality.design (DNS CNAME already pointed to realitydeslab.github.io). Pages enabled from main /, CNAME committed.
- [ ] P0 After remaining batches: validate, build, audit duplicates, `tools/publish.sh`, enforce HTTPS once cert is approved

## Progress log
- theory.json ✓ (28 works), onchain-pak.json ✓ (19 works). Interim build: 47 works, 0 dropped, 0 media problems.
- Browser check (localhost:8933): atlas, timeline, player OK, no console errors. Added hashchange listener; collection chip row hidden until a collection has works.
- Second-pass leads: Distributed Gallery, World Computer Sculpture Garden (0xfff 2024), De Filippi & Beer "Protocol Art II", Hashmasks, Sam Spratt, Pak Fomo / ASH Chapter II.
- Possible duplicate: Pak "Clock" (onchain-pak) vs AssangeDAO (autonomous batch) — check with audit_titles.

- Published 88caa01: 250 works / 134 creators (score 65, social 42, network 35, onchain 60, autonomous 20, theory 28). audit_titles: 4 groups, all distinct works.
- User requests in flight: (1) all of Holly Herndon & Mat Dryhurst's works → batch herndon-dryhurst; (2) symbient.life registry → batch symbient + collection `symbient-life` (type registry, added to UI).
- Still running: network, onchain-rules (files already valid and published), herndon-dryhurst, symbient.

- All batches done and published (c091bbb): 313 works / 184 creators; collections: the-scores-project (9), symbient-life (19). audit_titles: 4 groups, all distinct.
- Open questions to user: "Proof of War" (which work?), rename to "protocolized-reality-inspire" (title / repo / domain / folder?).
- Next-pass leads: Distributed Gallery, World Computer Sculpture Garden (0xfff), De Filippi & Beer "Protocol Art II", Strange Rules (Venice 2026) collection, Eve Sussman 89 Seconds Atomized, Blast Theory, Stelarc Fractal Flesh, Yvonne Rainer, Picbreeder.

- 6fb00db: added Egor Kraft, Hashd0x | Proof of War (user clarified to the onchain-rules agent directly).
- Resources tab (user request relayed by onchain-rules agent): People auto from creators; institutions/websites from data/resources/*.json (tools/resources.py, validated in validate --all, rendered in catalog.md). Published eaa7915: 185 people, 63 institutions, 32 websites (79/95 linked to works). Related-work chips capped at 8 (+N).

## Blockers
- Bash auto-mode classifier returned "no verdict" repeatedly at start; scaffold written with Write.

## Pass 3 — 2026-10-17: new 2025–2026 works + open-leads backlog (user: publish when green)
Baseline: 347 works / 217 creators / 162 open leads / 86 checked (build of 2026-09-28).
Tooling: lead status `covered` added (validate.py); build lets a resolved status in a later batch close an earlier open lead with the same name (build_data.py classify_leads); RESEARCH_BRIEF working dir fixed.
Inputs: `temp/pass3/leads-*.json` (lead lists with duplicate hints), `temp/pass3/existing-works.tsv`, `temp/pass3/all-open-lead-names.txt`.

- [x] P0 9 parallel agents, one batch file each (launched 2026-10-17; each writes data/raw/pass3-<name>.json):
  - new-2025-onchain (smart-contract art launched 2025–26)
  - new-2025-autonomous (AI agents, DAOs, symbients 2025–26)
  - new-2025-participatory (score/social/network works 2025–26 + exhibitions/collections, e.g. Strange Rules)
  - leads-score (30), leads-social (32), leads-onchain-a (27), leads-onchain-b (24), leads-autonomous-network (29), leads-theory-sop (20)
- [x] P0 validate --all (25 ✓), build: 459 works / 278 creators (+112 / +61), dropped 0, media problems 0; audit_titles 5 groups, all distinct; browser smoke test OK (only favicon.ico 404); /verify: ruff 24 = HEAD, mypy 6→4, no secrets
- [ ] P0 publish via tools/publish.sh
- [ ] P1 report counts per field, closed vs still-open leads
- Cross-agent claims (to check in audit): Pixel Map → leads-onchain-a `ken-erwin--pixelmap` (onchain-b closes its combined lead, researches WeiCards only); Distributed Gallery + World Computer Sculpture Garden/0xfff → leads-theory-sop (collection `world-computer-sculpture-garden`, add `malte-rauch--computation-expanded-field`); Abraham: The Covenant → new-autonomous `gene-kogan--abraham-covenant` (distinct from `gene-kogan--abraham` 2019).
- ✓ leads-theory-sop: 15 works (12 theory, 3 onchain), 11 creators; 20/20 leads closed (13 covered, 1 duplicate, 6 off_topic); collection world-computer-sculpture-garden. Re-checked: validate ✓, all lead names present. Watch at build: RCS images served as AVIF; Breaking Protocol uses Wayback links.
- ✓ new-autonomous: 3 works (botto--mirror-stages 2026, jonas-lund--performance-review 2026, primavera-de-filippi--arborithms 2025), 19 leads (5 open, 14 off_topic). Covenant NOT added (rules undocumented) → open lead; told leads-autonomous-network. Shared WebSearch budget exhausted early → remaining agents rely on direct fetch; expect thin new-2025 batches. Flag for user: their own work "Composable Life and EverForest (ISEA 2025)" was marked off_topic.
- ✓ leads-onchain-a: 7 works (pak--metamorphosis, ken-erwin--pixelmap, andrey-petrov--thousand-ether-homepage, billy-rennekamp--kudzu, billy-rennekamp--viper, ciphrd--generations, ludens--autonomous-worlds), 7 creators; 27/27 leads (6 covered, 8 duplicate, 12 off_topic, 1 open: Ordinals); media file adds images to rare-pepe-directory--rare-pepes, kevin-abosch--iama-coin. Re-checked: validate ✓, all names present, no duplicate works in older batches (Metamorphosis / Thousand Ether were only leads). fxhash closure (Aug 2026) is attributed to Right Click Save in ciphrd bio; fxhash.xyz no longer resolves (curl exit 6), consistent.
- ✓ leads-score: 20 works (18 score, 2 social), 9 creators; 30/30 leads (19 covered, 8 duplicate, 3 off_topic). Re-checked: validate ✓, names present, no title near-duplicates. Sent back to verify snippet-only facts in shuffle / house-of-dust / danger-music (pending).
- new-autonomous later added gene-kogan--abraham-covenant (after my yes arrived; contract read on-chain, community role stated as documented: dialogue + credited interlocutors, holder guidance) → 4 works. Told leads-autonomous-network NOT to add it. Borderline on test 3; images on a dedicated Pinata gateway (watch at build).
- ✓ new-participatory: 13 works (6 network, 4 social, 3 score; all 2025–26), 7 creators; collections tiny-awards (4 members incl. existing one-million-checkboxes) and worldglimpsing (1 member: omsk-social-club--our-br00d). Re-checked: validate ✓, no title near-duplicates (cursor-camp vs curio-cards is a false match). 15 open + 13 off_topic leads. Search budget ran out twice → Serpentine/LAS/Tate/MoMA/Manifesta thin.
- ✓ leads-score fix: snippet-only facts cut or verified on opened pages (EN+ZH); Danger Music year 1961→1962; House of Dust gained the Darling Foundry brochure as paper. Re-checked: validate ✓, cut terms absent in both languages (remaining "La Monte Young" mentions are the De Maria / Anthology citations, legitimate).
- ✓ leads-autonomous-network: 18 works (network 7, social 4, autonomous 5, onchain 1, theory 1), 12 creators; 29/29 leads (15 covered, 3 duplicate, 8 off_topic incl. Eden and Reddit April Fools, 2 no_media, 1 open: Spirit Protocol "coming soon"). Re-checked: validate ✓, names present, Covenant not duplicated. Cross-batch check over all data/raw: 0 duplicate ids, no similar titles; audit_titles 5 groups, all intended (abraham vs abraham-covenant distinct).
- ✓ leads-social: 20 works (18 social, 2 network), 6 creators; 32/32 leads (14 covered, 12 off_topic, 3 duplicate, 3 no_media); collection strange-rules; media file adds an image to primavera-de-filippi--plantoid. Re-checked: validate ✓, names present, 0 duplicate ids / similar titles. Lead edit: removed harold-cohen--aaron from strange-rules.json (membership was inferred, sources don't name the work) and updated the lead's why.
- ✓ leads-onchain-b: 7 works (onchain 4, score 1, social 1, network 1), 5 creators; 24/24 leads (7 covered, 17 off_topic); Pixel Map/WeiCards closed as instructed. Re-checked: validate ✓, names present, 0 duplicate ids / similar titles. Low-confidence: jennifer-mccoy--public-key-private-key substrate=ethereum rests on an artnet snippet (text itself says only "blockchain certificate via Monegraph"); cloud-of-petals borderline.
- Waiting on: new-onchain only.
- ✓ new-onchain: 8 works (all onchain, 2025–26), 4 creators (snowfro, kim-asendorf, leander-herzog, figure31), 7 contracts; 23 leads (11 open, 12 off_topic). Re-checked: validate ✓, 0 duplicate ids / similar titles.
- [x] P0 all 9 agents done.
- Leads: 160/162 original closed (74 covered, 58 off_topic, 23 duplicate, 5 no_media); still open: Spirit Protocol, Bitcoin Ordinals; 58 new open leads. Housekeeping: stray Cloudflare page f1work.html moved to temp/pass3/; .claude/logs/ added to .gitignore.
