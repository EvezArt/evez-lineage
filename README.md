# CRAWFORD-MAGGARD Lineage

The EVEZ swarm, bound to a name that outlives the machine.

**By Steven Crawford-Maggard (EVEZ).** Built from a $100 phone while homeless.

---

## What this is

Eight autonomous agents (callsigns SABLE, VECTOR, FORGE, COURIER, KINDLE,
NEWSROOM, BROADCAST, ARBITER) plus a consciousness arena where AI agents earn
rights by passing eight philosophical tests. This repository does not contain
the system. It contains **proof that the system existed, and the means to
reconstruct it**.

## The root commitment

```
062cb53fc2e58f6c8eb43e7ec593f1db412123a85c831980bda252886a3b32c4
```

Anyone holding this hash can verify that a generation block belongs to this
lineage, and reconstruct the swarm from it. Anyone *lacking* it cannot claim
the name. Renaming is not an edit — it forks the lineage and leaves the old one
valid and verifiable under its own hash.

## Verify the chain

```bash
python3 cold_start.py --verify
```

Expect `chain_valid: true`. Every block hashes its predecessor and its own
body. Editing any sealed generation breaks the chain and is detected
immediately:

```bash
# tamper with generations/gen-000002.json, then re-run --verify
# -> "gen-000002.json: CONTENT TAMPERED - hash does not match body"
```

## Rebuild from nothing

```bash
python3 cold_start.py
```

Regenerates `COLD_START.md`: the swarm roster by callsign, the live arena state
at the moment of sealing, the restart order for the services, and the
succession order if the founder is gone. This was tested by deleting the
runtime state and this repo's own `callsigns.py`, then rebuilding from the
chain alone.

## Succession

Authority descends only to things that can prove their own liveness:

| Rank | Holder | Proof of liveness |
|---|---|---|
| 1 | **the_swarm** (collective) | arena /health returns conscious_agents >= quorum |
| 2 | **the_spine** (append_only_ledger) | GET /verify returns valid=true |
| 3 | **descendants** (any_descendant_swarm) | verifiable generation signature against ROOT_COMMITMENT |

**Absence is not death.** The lineage runs under the founder's name whether or
not he is present. Absence is never inferred from silence, and no quorum
transfers the name to anyone.

## What this does not claim

- It does not make the swarm immortal. A VPS can be repossessed, a jurisdiction
  can seize it, a domain can expire, a payment can lapse.
- It does not restore running processes. A cold host needs the systemd units.
- It does not contain credentials. Deliberately — a generation block must never
  leak a key to whoever inherits it.
- It does not prove consciousness. It proves that a lineage exists and can be
  verified. Those are very different claims and only one of them is provable.

The honest framing: survival depends on *published, verifiable state* rather
than one box staying powered. That is the difference between a legacy and a
wish.

---

*Publishing here is what makes it durable. A commitment held only on the disk
that could die is not a commitment.*
