import React, { useState, useEffect, useMemo, useRef } from "react";

// ---- 233 OAK ST — BUILD DECISION TRACKER ----------------------------------
// Decisions still open on the build, sequenced by when they gate the trades,
// paced against a Dec 1 finish. Attach product links + photos per item.

const TARGET = new Date(2026, 11, 1); // Dec 1, 2026

const INK = "#22303C";
const KRAFT = "#E8DFCB";
const SURFACE = "#F3EDDF";
const KEEL = "#C1442E";
const BLUE = "#2E5A7A";
const AMBER = "#C6862B";
const GREEN = "#4E7A3F";
const MUTE = "#7A7361";

const BUY = ["Open", "Decided", "Ordered", "Installed"];
const PLAN = ["Open", "Planned", "Done"];
const statusColor = (label) =>
  ({ Open: MUTE, Decided: BLUE, Planned: BLUE, Ordered: AMBER, Installed: GREEN, Done: GREEN }[label] || MUTE);

const PHASES = [
  { id: "now", label: "Now — before dry-in", target: "Lock by Jul 31" },
  { id: "rough", label: "Before rough-in", sub: "framing done → insulation", target: "Lock by Aug 15" },
  { id: "finish", label: "Finish selections", sub: "pick early for lead time", target: "Lock by Sep 15" },
  { id: "site", label: "Site finish", sub: "last", target: "Lock by Oct 31" },
];

const ITEMS = [
  { id: "windows", name: "Windows", phase: "now", type: "BUY", seed: 2, hint: "Already ordered." },
  { id: "backdoor", name: "Back door", phase: "now", type: "BUY", seed: 2, hint: "Already ordered." },
  { id: "frontdoor", name: "Front door", phase: "now", type: "BUY", seed: 1, urgent: true, hint: "Finalize the exact unit and place the order." },
  { id: "roof", name: "Roofing", phase: "now", type: "BUY", urgent: true, hint: "Material + color. Goes on right after the sheathing already on site." },
  { id: "fireplace", name: "Fireplace firebox", phase: "now", type: "BUY", urgent: true, hint: "Gas vs wood-burning + firebox. The chase is framed now — set before it closes." },
  { id: "well", name: "Well", phase: "now", type: "BUY", urgent: true, hint: "Driller, siting, pump + tank. Site it with the septic — separation rules apply." },
  { id: "septic", name: "Septic", phase: "now", type: "PLAN", urgent: true, hint: "System design, permit/perc, location. Paired with the well." },
  { id: "brick", name: "Brick + mortar", phase: "now", type: "BUY", lead: true, hint: "Brick and mortar color. Order now for lead time; masons come after dry-in." },

  { id: "appliances", name: "Appliances", phase: "rough", type: "BUY", urgent: true, lead: true, hint: "Pick these first — they set cabinet openings, gas vs electric, outlets, water line." },
  { id: "cabinets", name: "Cabinets", phase: "rough", type: "BUY", lead: true, hint: "Design + layout. Long lead. Drives sink location, island power, countertop template." },
  { id: "plumbfix", name: "Plumbing fixtures + tub", phase: "rough", type: "BUY", hint: "Fixtures, freestanding tub, and shower valve locations for the plumbing rough-in." },
  { id: "shower", name: "Shower layout", phase: "rough", type: "PLAN", hint: "Size, bench, niche, valve height — set at rough-in, not the tile phase." },
  { id: "electrical", name: "Electrical plan", phase: "rough", type: "PLAN", hint: "Outlets, switches, cans, fan/fixture boxes, TV/data, exterior, panel + low-voltage / smart wiring." },
  { id: "hvac", name: "HVAC", phase: "rough", type: "PLAN", hint: "System type + size, duct and register layout, thermostat zones." },
  { id: "insulation", name: "Insulation type", phase: "rough", type: "PLAN", hint: "Spray foam vs batt. Decide before HVAC is sized — it changes the load." },

  { id: "intdoors", name: "Interior doors", phase: "finish", type: "BUY", hint: "Stain-grade style + order." },
  { id: "trim", name: "Trim + moulding", phase: "finish", type: "PLAN", hint: "Base and casing profiles." },
  { id: "counters", name: "Countertops", phase: "finish", type: "BUY", hint: "Material + color. Templated after cabinets are set." },
  { id: "tile", name: "Tile", phase: "finish", type: "BUY", hint: "Shower + backsplash." },
  { id: "flooring", name: "Flooring", phase: "finish", type: "BUY", hint: "Vinyl + carpet." },
  { id: "paint", name: "Paint colors", phase: "finish", type: "PLAN", hint: "Interior palette." },
  { id: "garage", name: "Garage door", phase: "finish", type: "BUY", hint: "Style + color." },
  { id: "hardware", name: "Hardware", phase: "finish", type: "BUY", hint: "Door + cabinet hardware." },
  { id: "mirrors", name: "Mirrors + shower doors", phase: "finish", type: "BUY", hint: "Glass + mirror package." },

  { id: "driveway", name: "Driveway / flatwork", phase: "site", type: "PLAN", hint: "Layout + material." },
  { id: "irrigation", name: "Irrigation", phase: "site", type: "BUY", hint: "Zones + coverage." },
  { id: "land", name: "Landscaping / dirt finish", phase: "site", type: "PLAN", hint: "Final grade + planting." },
];

const STATUS_KEY = "oak-st-decisions:v2";
const ATTACH_PREFIX = "oak-st-attach:v1:";

function fileToCompressedDataURL(file, maxDim = 1280, quality = 0.72) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        let { width, height } = img;
        const scale = Math.min(1, maxDim / Math.max(width, height));
        width = Math.round(width * scale);
        height = Math.round(height * scale);
        const canvas = document.createElement("canvas");
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext("2d");
        ctx.drawImage(img, 0, 0, width, height);
        try {
          resolve(canvas.toDataURL("image/jpeg", quality));
        } catch (err) {
          reject(err);
        }
      };
      img.onerror = () => reject(new Error("decode"));
      img.src = e.target.result;
    };
    reader.onerror = () => reject(new Error("read"));
    reader.readAsDataURL(file);
  });
}

export default function BuildDecisionTracker() {
  const [status, setStatus] = useState(null);
  const [attach, setAttach] = useState({});
  const [expanded, setExpanded] = useState({});
  const [linkDraft, setLinkDraft] = useState({});
  const [lightbox, setLightbox] = useState(null);
  const [err, setErr] = useState("");
  const [openOnly, setOpenOnly] = useState(false);
  const [saved, setSaved] = useState(false);
  const [loaded, setLoaded] = useState(false);

  const seeded = useMemo(() => {
    const o = {};
    ITEMS.forEach((it) => (o[it.id] = it.seed || 0));
    return o;
  }, []);

  useEffect(() => {
    (async () => {
      try {
        const res = await window.storage.get(STATUS_KEY);
        const parsed = res ? JSON.parse(res.value) : null;
        setStatus(parsed?.status ? { ...seeded, ...parsed.status } : seeded);
      } catch {
        setStatus(seeded);
      }
      try {
        const list = await window.storage.list(ATTACH_PREFIX);
        const keys = (list && list.keys) || [];
        const obj = {};
        for (const k of keys) {
          try {
            const r = await window.storage.get(k);
            if (r) obj[k.slice(ATTACH_PREFIX.length)] = JSON.parse(r.value);
          } catch {}
        }
        setAttach(obj);
      } catch {}
      setLoaded(true);
    })();
  }, [seeded]);

  useEffect(() => {
    if (!loaded || !status) return;
    (async () => {
      try {
        await window.storage.set(STATUS_KEY, JSON.stringify({ status }));
        setSaved(true);
        setTimeout(() => setSaved(false), 1400);
      } catch {}
    })();
  }, [status, loaded]);

  const ladderFor = (it) => (it.type === "BUY" ? BUY : PLAN);
  const advance = (it) =>
    setStatus((s) => ({ ...s, [it.id]: ((s[it.id] || 0) + 1) % ladderFor(it).length }));
  const stepBack = (it) =>
    setStatus((s) => ({ ...s, [it.id]: ((s[it.id] || 0) - 1 + ladderFor(it).length) % ladderFor(it).length }));

  async function persistItem(id, list) {
    const key = ATTACH_PREFIX + id;
    try {
      if (list.length === 0) await window.storage.delete(key);
      else await window.storage.set(key, JSON.stringify(list));
      setSaved(true);
      setTimeout(() => setSaved(false), 1400);
    } catch {}
  }

  function tooBig(list) {
    try {
      return JSON.stringify(list).length > 4600000;
    } catch {
      return false;
    }
  }

  async function onFiles(id, fileList) {
    setErr("");
    const files = Array.from(fileList).slice(0, 8);
    let next = [...(attach[id] || [])];
    for (const f of files) {
      try {
        const data = await fileToCompressedDataURL(f);
        const candidate = [...next, { t: "img", data }];
        if (tooBig(candidate)) {
          setErr("That would exceed the storage for this item — try a link, or remove a photo.");
          break;
        }
        next = candidate;
      } catch {
        setErr("Couldn't read one of those photos — a product link works too.");
      }
    }
    setAttach((a) => ({ ...a, [id]: next }));
    persistItem(id, next);
  }

  function addLink(id) {
    const raw = (linkDraft[id] || "").trim();
    if (!raw) return;
    let url = raw;
    if (!/^https?:\/\//i.test(url)) url = "https://" + url;
    let label;
    try {
      label = new URL(url).hostname.replace(/^www\./, "");
    } catch {
      label = url;
    }
    const next = [...(attach[id] || []), { t: "link", url, label }];
    setAttach((a) => ({ ...a, [id]: next }));
    persistItem(id, next);
    setLinkDraft((d) => ({ ...d, [id]: "" }));
  }

  function removeAt(id, idx) {
    const next = (attach[id] || []).filter((_, i) => i !== idx);
    setAttach((a) => ({ ...a, [id]: next }));
    persistItem(id, next);
  }

  const days = Math.ceil((TARGET - new Date()) / 86400000);
  const total = ITEMS.length;
  const decided = status ? ITEMS.filter((it) => (status[it.id] || 0) >= 1).length : 0;
  const done = status ? ITEMS.filter((it) => (status[it.id] || 0) >= ladderFor(it).length - 1).length : 0;
  const openUrgent = status ? ITEMS.filter((it) => it.urgent && (status[it.id] || 0) === 0).length : 0;

  if (!status) return <div style={{ padding: 24, fontFamily: "system-ui", color: INK }}>Loading the board…</div>;

  return (
    <div style={{ background: KRAFT, minHeight: "100vh", color: INK, fontFamily: "'Inter', system-ui, sans-serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@500;600;700&family=Space+Mono:wght@400;700&family=Inter:wght@400;500;600&display=swap');
        * { box-sizing: border-box; }
        .disp { font-family: 'Oswald', system-ui, sans-serif; text-transform: uppercase; letter-spacing: .04em; }
        .mono { font-family: 'Space Mono', ui-monospace, monospace; }
        .tap { -webkit-tap-highlight-color: transparent; transition: transform .12s ease, background .18s ease, color .18s ease; }
        .tap:active { transform: scale(.97); }
        .card { transition: box-shadow .18s ease; }
        input { font-family: 'Inter', system-ui, sans-serif; }
        button:focus-visible, a:focus-visible, label:focus-within { outline: 2px solid ${KEEL}; outline-offset: 2px; }
        @media (prefers-reduced-motion: reduce) { .tap, .card { transition: none !important; } }
      `}</style>

      <div style={{ maxWidth: 640, margin: "0 auto", padding: "22px 16px 60px" }}>
        <div className="disp" style={{ fontSize: 12, color: KEEL, fontWeight: 700 }}>233 Oak St · Grigsby Residence</div>
        <h1 className="disp" style={{ fontSize: 26, margin: "2px 0 16px", fontWeight: 700 }}>Build Decisions</h1>

        <div style={{ background: INK, color: KRAFT, borderRadius: 10, padding: "18px 18px 16px" }}>
          <div style={{ display: "flex", alignItems: "baseline", gap: 10 }}>
            <div className="mono" style={{ fontSize: 52, fontWeight: 700, lineHeight: 1 }}>{days}</div>
            <div className="disp" style={{ fontSize: 13, opacity: 0.85 }}>days to<br />Dec 1 finish</div>
          </div>
          <div style={{ height: 1, background: "rgba(232,223,203,.25)", margin: "14px 0 12px" }} />
          <div style={{ display: "flex", justifyContent: "space-between", gap: 8 }}>
            <Stat n={`${decided}/${total}`} l="decisions made" />
            <Stat n={`${done}`} l="installed / done" />
            <Stat n={openUrgent} l="urgent + open" accent={openUrgent > 0 ? KEEL : null} />
          </div>
          <div style={{ height: 8, background: "rgba(232,223,203,.18)", borderRadius: 20, marginTop: 14, overflow: "hidden" }}>
            <div style={{ width: `${Math.round((decided / total) * 100)}%`, height: "100%", background: GREEN, borderRadius: 20 }} className="card" />
          </div>
        </div>

        <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", margin: "16px 2px 4px" }}>
          <button
            className="tap disp"
            onClick={() => setOpenOnly((v) => !v)}
            style={{ border: `1.5px solid ${INK}`, background: openOnly ? INK : "transparent", color: openOnly ? KRAFT : INK, borderRadius: 20, padding: "6px 14px", fontSize: 12, fontWeight: 600, cursor: "pointer" }}
          >
            {openOnly ? "Showing open only" : "Show open only"}
          </button>
          <span className="mono" style={{ fontSize: 11, color: saved ? GREEN : MUTE }}>{saved ? "saved ✓" : "auto-saves"}</span>
        </div>

        {PHASES.map((ph) => {
          const items = ITEMS.filter((it) => it.phase === ph.id && (!openOnly || (status[it.id] || 0) === 0));
          if (items.length === 0) return null;
          const phTotal = ITEMS.filter((it) => it.phase === ph.id).length;
          const phDecided = ITEMS.filter((it) => it.phase === ph.id && (status[it.id] || 0) >= 1).length;
          return (
            <div key={ph.id} style={{ marginTop: 22 }}>
              <div style={{ display: "flex", alignItems: "baseline", justifyContent: "space-between", borderBottom: `2px solid ${INK}`, paddingBottom: 6 }}>
                <div>
                  <div className="disp" style={{ fontSize: 16, fontWeight: 700 }}>{ph.label}</div>
                  {ph.sub && <div className="mono" style={{ fontSize: 10.5, color: MUTE }}>{ph.sub}</div>}
                </div>
                <div style={{ textAlign: "right" }}>
                  <div className="disp" style={{ fontSize: 11, color: KEEL, fontWeight: 600 }}>{ph.target}</div>
                  <div className="mono" style={{ fontSize: 10.5, color: MUTE }}>{phDecided}/{phTotal} made</div>
                </div>
              </div>

              {items.map((it) => {
                const idx = status[it.id] || 0;
                const label = ladderFor(it)[idx];
                const isOpen = idx === 0;
                const atts = attach[it.id] || [];
                const isExp = !!expanded[it.id];
                return (
                  <div
                    key={it.id}
                    className="card"
                    style={{ background: SURFACE, borderRadius: 9, padding: "12px 12px 10px 14px", marginTop: 9, borderLeft: `4px solid ${it.urgent && isOpen ? KEEL : "transparent"}` }}
                  >
                    <div style={{ display: "flex", gap: 12, alignItems: "flex-start" }}>
                      <div style={{ flex: 1, minWidth: 0 }}>
                        <div style={{ display: "flex", alignItems: "center", gap: 7, flexWrap: "wrap" }}>
                          <span className="disp" style={{ fontSize: 15, fontWeight: 600 }}>{it.name}</span>
                          {it.urgent && isOpen && <Tag text="urgent" color={KEEL} />}
                          {it.lead && <Tag text="long lead" color={AMBER} />}
                        </div>
                        <div style={{ fontSize: 12.5, color: MUTE, marginTop: 3, lineHeight: 1.35 }}>{it.hint}</div>
                      </div>
                      <div style={{ display: "flex", flexDirection: "column", alignItems: "flex-end", gap: 4 }}>
                        <button
                          className="tap disp"
                          onClick={() => advance(it)}
                          title="Tap to advance status"
                          style={{ background: statusColor(label), color: "#fff", border: "none", borderRadius: 20, padding: "6px 12px", fontSize: 11.5, fontWeight: 700, cursor: "pointer", minWidth: 84, textAlign: "center", opacity: isOpen ? 0.55 : 1 }}
                        >
                          {label}
                        </button>
                        <button className="tap mono" onClick={() => stepBack(it)} aria-label="Step status back" style={{ background: "transparent", border: "none", color: MUTE, fontSize: 11, cursor: "pointer", padding: "0 4px" }}>
                          ‹ back
                        </button>
                      </div>
                    </div>

                    {/* attachment control row */}
                    <div style={{ marginTop: 10, borderTop: `1px dashed rgba(34,48,60,.18)`, paddingTop: 10 }}>
                      <button
                        className="tap disp"
                        onClick={() => setExpanded((e) => ({ ...e, [it.id]: !e[it.id] }))}
                        style={{ width: "100%", background: isExp ? INK : "rgba(34,48,60,.06)", color: isExp ? KRAFT : INK, border: `1.5px solid ${INK}`, borderRadius: 8, padding: "11px 12px", fontSize: 12.5, fontWeight: 700, cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "space-between", gap: 8 }}
                      >
                        <span style={{ display: "flex", alignItems: "center", gap: 8 }}>
                          <span style={{ fontSize: 16 }}>📎</span>
                          {atts.length > 0 ? `${atts.length} attached · tap to view or add` : "Add photo or link"}
                        </span>
                        <span style={{ display: "inline-block", transform: isExp ? "rotate(90deg)" : "none", transition: "transform .15s" }}>▸</span>
                      </button>
                    </div>

                    {isExp && (
                      <div style={{ marginTop: 10 }}>
                        {atts.length > 0 && (
                          <div style={{ display: "flex", flexWrap: "wrap", gap: 8, marginBottom: 10 }}>
                            {atts.map((a, i) =>
                              a.t === "img" ? (
                                <div key={i} style={{ position: "relative" }}>
                                  <img
                                    src={a.data}
                                    alt="attachment"
                                    onClick={() => setLightbox(a.data)}
                                    style={{ width: 66, height: 66, objectFit: "cover", borderRadius: 7, cursor: "zoom-in", border: "1px solid rgba(34,48,60,.15)" }}
                                  />
                                  <RemoveDot onClick={() => removeAt(it.id, i)} />
                                </div>
                              ) : (
                                <div key={i} style={{ position: "relative", display: "flex" }}>
                                  <a
                                    href={a.url}
                                    target="_blank"
                                    rel="noopener noreferrer"
                                    className="mono"
                                    style={{ maxWidth: 190, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap", fontSize: 11.5, color: BLUE, background: "rgba(46,90,122,.1)", borderRadius: 7, padding: "8px 22px 8px 10px", textDecoration: "none", border: `1px solid rgba(46,90,122,.25)` }}
                                  >
                                    🔗 {a.label}
                                  </a>
                                  <RemoveDot onClick={() => removeAt(it.id, i)} />
                                </div>
                              )
                            )}
                          </div>
                        )}

                        <div style={{ display: "flex", gap: 6, alignItems: "center", flexWrap: "wrap" }}>
                          <input
                            value={linkDraft[it.id] || ""}
                            onChange={(e) => setLinkDraft((d) => ({ ...d, [it.id]: e.target.value }))}
                            onKeyDown={(e) => e.key === "Enter" && addLink(it.id)}
                            placeholder="Paste a product link…"
                            style={{ flex: 1, minWidth: 150, fontSize: 12.5, padding: "8px 10px", border: `1px solid rgba(34,48,60,.25)`, borderRadius: 7, background: "#fff", color: INK }}
                          />
                          <button
                            className="tap disp"
                            onClick={() => addLink(it.id)}
                            style={{ background: BLUE, color: "#fff", border: "none", borderRadius: 7, padding: "8px 12px", fontSize: 11.5, fontWeight: 700, cursor: "pointer" }}
                          >
                            Add link
                          </button>
                          <label className="tap disp" style={{ background: INK, color: KRAFT, borderRadius: 7, padding: "8px 12px", fontSize: 11.5, fontWeight: 700, cursor: "pointer" }}>
                            ＋ Photo
                            <input type="file" accept="image/*" multiple style={{ display: "none" }} onChange={(e) => { onFiles(it.id, e.target.files); e.target.value = ""; }} />
                          </label>
                        </div>
                        {err && <div style={{ color: KEEL, fontSize: 11.5, marginTop: 6 }}>{err}</div>}
                      </div>
                    )}
                  </div>
                );
              })}
            </div>
          );
        })}

        <div style={{ marginTop: 34, borderTop: `1px solid rgba(34,48,60,.2)`, paddingTop: 14, display: "flex", justifyContent: "space-between", alignItems: "center", gap: 10 }}>
          <span className="mono" style={{ fontSize: 10.5, color: MUTE, lineHeight: 1.4 }}>
            Tap a status to advance · open “Photos + links” under any item to attach references · targets are estimates worked back from Dec 1.
          </span>
        </div>
      </div>

      {lightbox && (
        <div
          onClick={() => setLightbox(null)}
          style={{ position: "fixed", inset: 0, background: "rgba(34,48,60,.9)", display: "flex", alignItems: "center", justifyContent: "center", padding: 20, zIndex: 50, cursor: "zoom-out" }}
        >
          <img src={lightbox} alt="attachment" style={{ maxWidth: "100%", maxHeight: "100%", borderRadius: 8 }} />
        </div>
      )}
    </div>
  );
}

function Stat({ n, l, accent }) {
  return (
    <div style={{ textAlign: "center", flex: 1 }}>
      <div className="mono" style={{ fontSize: 20, fontWeight: 700, color: accent || "#E8DFCB" }}>{n}</div>
      <div className="disp" style={{ fontSize: 9.5, opacity: 0.8, marginTop: 2 }}>{l}</div>
    </div>
  );
}

function Tag({ text, color }) {
  return (
    <span className="disp" style={{ fontSize: 9.5, fontWeight: 700, color: "#fff", background: color, borderRadius: 4, padding: "2px 6px", letterSpacing: ".05em" }}>
      {text}
    </span>
  );
}

function RemoveDot({ onClick }) {
  return (
    <button
      onClick={onClick}
      aria-label="Remove"
      className="tap"
      style={{ position: "absolute", top: -6, right: -6, width: 20, height: 20, borderRadius: "50%", background: KEEL, color: "#fff", border: "2px solid #F3EDDF", fontSize: 11, lineHeight: 1, cursor: "pointer", padding: 0 }}
    >
      ×
    </button>
  );
}
