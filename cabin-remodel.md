# Cabin remodel — task map (Mermaid)

**If the diagrams below show as code blocks:** Cursor’s default Markdown preview does not run Mermaid. Use either:

1. Install the extension **Markdown Preview Mermaid Support** (or **Mermaid Preview**), then open Markdown preview, or  
2. Open **`index.html`** in your browser. On the live page you can **tap any flowchart box or Gantt label/bar** for scope notes, or use the **task list** at the bottom (good on phones).

The flowchart uses **line breaks** in labels (`<br/>`). If preview strips them, open the HTML file or set Mermaid `securityLevel: loose` in your preview settings.

---

## Flowchart

```mermaid
%%{init: {"flowchart": {"htmlLabels": true, "padding": 20, "nodeSpacing": 55, "rankSpacing": 50}}}%%
flowchart TB
    subgraph P1["1 · Dry crawlspace"]
        direction LR
        D1["Drainage<br/>if needed"]
        D2["Sump pump<br/>if needed"]
        D1 --- D2
    end

    subgraph P2["2 · Framing & structure"]
        direction TB
        W1["Replace joists"]
        W2["Replace rim joist"]
        W3["Beams & piers level"]
        W1 -.->|same crew| W2
        W1 -.->|same phase| W3
        W2 -.->|same phase| W3
    end

    subgraph P2U["Washer · rough utilities"]
        WPLUMB["Washer water<br/>& drain"]
        WELEC["Washer ·<br/>new circuit"]
    end

    subgraph P3["3 · Slab / stone<br/>if needed"]
        C1["Pour or cap<br/>rubble areas"]
    end

    subgraph P4["4 · Encapsulation"]
        direction TB
        E1["Mat + vapor<br/>barrier"]
        E2["Wall insulation"]
        E3["Dehumidifier<br/>seal vents"]
        E1 --> E2
        E1 --> E3
    end

    subgraph P5["5 · Kitchen & main floors"]
        direction TB
        F0["Crawlspace closed<br/>floors can open"]
        F1["Strip extra<br/>kitchen layers"]
        F2["Fir patches"]
        F3["Sand & refinish<br/>wood floors"]
        F4["Prep · door tile"]
        F5["Tile · interior door"]

        F0 --> F1
        F1 --> F2
        F2 --> F3
        F2 --> F4
        F4 --> F5
        F3 -.->|meet at transition| F5
    end

    subgraph P5B["5B · Bathroom"]
        direction TB
        F6["Strip bath<br/>subfloor ×2"]
        TUB["Install tub"]
        F7["Heat wire + prep"]
        F8["Bath floor tile"]
        BWT["Tub surround tile"]
        SD["Shower door"]
        BFAN["Bath exhaust fan"]
        BVF["Vanity · toilet · bath trim"]

        F6 --> TUB
        TUB --> F7
        F7 --> F8
        F8 --> BWT
        BWT --> SD
        SD --> BFAN
        F8 --> BVF
    end

    subgraph P6["6 · Kitchen finish"]
        K1["Cabinets<br/>(dishwasher space)"]
        KSVC["Circuits · counter<br/>hood · DW"]
        CTOP["Countertops"]
        KSINK["Replace sink"]
        FAUCET["Kitchen faucet"]
        BACK["Backsplash"]
        DW["Dishwasher"]
        K1 --> KSVC
        KSVC --> CTOP
        KSVC --> KSINK
        CTOP -.->|same template day| KSINK
        CTOP --> FAUCET
        KSINK --> FAUCET
        FAUCET --> BACK
        CTOP --> DW
        KSVC --> DW
    end

    subgraph P9["Flexible timing · do subpanel first"]
        SP["New subpanel"]
        EL1["Lights & switches<br/>rough-in"]
        OUT["Outlets · devices<br/>tighten boxes"]
    end

    subgraph P8["8 · Ceiling & lights"]
        CHIM["Loft · cedar<br/>chimney patch"]
        CS0["Sand ceiling"]
        CS1["Clean ceiling<br/>Bar Keepers Friend"]
        CS2["Shellac ceiling"]
        LGT["Install fixtures"]
        CS0 --> CS1
        CHIM --> CS2
        EL1 --> CS2
        CS1 --> CS2
        CS2 --> LGT
        EL1 --> LGT
    end

    D1 --> W1
    D2 --> W1
    W3 --> C1
    W3 --> WPLUMB
    W3 --> WELEC
    SP --> WELEC
    C1 --> E1
    E2 --> F0
    E3 --> F0
    F2 --> F6
    F3 -.->|can overlap| F6
    F3 --> K1
    F5 --> K1
    SP --> KSVC
    SP --> BFAN
    F0 -.->|parallel OK| EL1
```

## Gantt (illustrative only)

Same **dependencies** as the flowchart. **Not a calendar commitment:** dummy start `2000-01-01`; **ignore axis dates**. **Bar lengths** are rough relative effort. Where tasks share the same **`after`** predecessor, Mermaid draws them **in parallel** (stacked)—that is “allowed overlap,” not a promise you will staff it that way.

```mermaid
gantt
    title Rough order only — not real dates
    dateFormat YYYY-MM-DD
    section Dry crawl
    Drains + sump           :a1, 2000-01-01, 36d
    section After dry parallel
    Subpanel                :sp, after a1, 14d
    Joists rim piers        :b1, after a1, 84d
    section Crawl parallel
    Washer plumbing         :wp, after b1, 21d
    Concrete / cap rubble   :c1, after b1, 28d
    Washer circuit          :wcirc, after wp after sp, 14d
    section Encapsulate
    Mat + barrier           :d1, after c1 after wp, 14d
    Wall insulation         :d2, after d1, 28d
    Dehu + seal vents       :d3, after d2, 12d
    section After encap parallel
    Lights rough-in         :el1, after d3, 42d
    Kitchen strip + fir     :e1, after d3, 48d
    Outlets refresh         :ou, after d3, 21d
    section Bathroom
    Strip bath floors       :ba, after e1, 14d
    New tub                 :bb, after ba, 24d
    Heat wire prep          :bc, after bb, 14d
    Bath floor tile         :bd, after bc, 24d
    Surround tile           :be, after bd, 28d
    Vanity + toilet         :bg, after bd, 24d
    Shower door             :bf, after be, 12d
    Bath exhaust fan        :bfan, after bf after sp, 10d
    section Wood floors
    Sand + refinish         :e2, after bfan after bg after bf, 42d
    Interior door tile      :e3, after e2, 18d
    section Ceiling
    Sand ceiling            :cs0, after e3, 14d
    Cedar chimney patch     :chim, after e3, 18d
    Ceiling clean BKF       :cs1, after cs0 after chim, 12d
    Shellac                 :cs2, after cs1 after el1 after chim, 18d
    Hang lights             :lg, after cs2 after el1, 12d
    section Kitchen
    Cabinets                :k1, after lg, 56d
    Kitchen new circuits    :k_elec, after k1 after sp, 18d
    Countertops             :k2, after k_elec, 42d
    Replace kitchen sink    :k_sink, after k_elec, 42d
    Kitchen faucet          :k_ft, after k2 after k_sink, 5d
    Backsplash              :k3, after k_ft, 21d
    Dishwasher              :k4, after k2, 10d
```

**Gantt notes:** **Subpanel** before bath fan. **Countertops** and **sink replace** share the same window (parallel after kitchen circuits); **faucet** after both; **backsplash** after faucet. Parallel tracks elsewhere: subpanel vs structure after dry; washer plumbing vs concrete; after encapsulation, lights rough-in + kitchen strip + outlets; after bath floor tile, surround vs vanity; fan after shower door + subpanel; after door tile, ceiling sand vs cedar patch; backsplash vs dishwasher after counters (DW can stay after counter only). Hired trades shorten **sp**, **wcirc**, **k_elec**. Multi-`after` needs a current Mermaid build.

## Grouping summary

| Group | Purpose |
|--------|--------|
| **1 Dry** | Stops moisture that rots wood and undermines encapsulation. |
| **2 Structure** | Joists, rim, beams/piers — same phase, often sequenced by access. |
| **2U Washer rough** | After **all crawlspace structural wood**: washer **sewer + supply** plumbing; **new washer circuit** needs **subpanel replaced** and wood work done. |
| **3 Rough areas** | Only if you need a stable surface before mat/plastic. |
| **4 Encapsulation** | Barrier, insulation, conditioning. |
| **5 Floors general** | Kitchen strip, fir, refinish, **interior door tile inside only** (feeds bath and kitchen). |
| **5B Bathroom** | Strip → tub → heat prep → floor tile → surround → shower door → **exhaust fan** (**subpanel** must be **done before** fan power). Vanity/toilet/trim can run parallel with surround from floor tile. |
| **6 Kitchen** | Cabinets → **kitchen circuits** (subpanel first). **Countertops** and **sink replacement** in the **same install window** (coordinate with fabricator). **Faucet** after counter + sink. **Backsplash** after faucet. **Dishwasher** after countertop (and circuits). |
| **8 Ceiling** | **Loft cedar** before shellac; sand → BKF → shellac; **install lights** after shellac **and** after rough-in complete. |
| **9 Anytime** | **Subpanel first** among these when you add circuits (**fan**, washer, kitchen). Then **light/switch rough-in** (no subpanel for that rough-in alone) and **outlets**. **Installing** lights waits on rough-in + shellac; **washer circuit** needs subpanel + crawl wood; **kitchen circuits** before backsplash/dishwasher. |

Adjust links into **K1** if kitchen cabinets must sit on tile vs refinished wood.
