import { useState } from "react";

const COLORS = {
  blue: "#2E86AB",
  green: "#06A77D",
  blueDark: "#1d6a8a",
  greenDark: "#058060",
  blueLight: "#5ba8c4",
  greenLight: "#38c99f",
  red: "#E84855",
  yellow: "#F4A261",
  dark: {
    bg: "#0d1117",
    surface: "#161b22",
    card: "#1c2330",
    border: "#2a3441",
    text: "#e6edf3",
    muted: "#8b949e",
    subtle: "#30363d",
  },
  light: {
    bg: "#f4f7fa",
    surface: "#ffffff",
    card: "#ffffff",
    border: "#e1e8ef",
    text: "#0d1117",
    muted: "#57606a",
    subtle: "#f0f4f8",
  },
};

const formatZAR = (n) =>
  "R" + n.toLocaleString("en-ZA", { minimumFractionDigits: 0, maximumFractionDigits: 0 });

// ─── Icons ───────────────────────────────────────────────────────────────────
const Icon = ({ name, size = 20, color = "currentColor" }) => {
  const paths = {
    home: "M3 9.5L12 3l9 6.5V20a1 1 0 01-1 1H14v-5h-4v5H4a1 1 0 01-1-1V9.5z",
    transactions: "M4 6h16M4 12h16M4 18h10",
    tax: "M9 14l2 2 4-4M7 3H5a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2V5a2 2 0 00-2-2h-2M9 3h6v4H9V3z",
    insights: "M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z",
    profile: "M20 21v-2a4 4 0 00-4-4H8a4 4 0 00-4 4v2M12 11a4 4 0 100-8 4 4 0 000 8z",
    check: "M5 13l4 4L19 7",
    arrow: "M9 18l6-6-6-6",
    arrowLeft: "M15 18l-6-6 6-6",
    sun: "M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z",
    moon: "M21 12.79A9 9 0 1111.21 3 7 7 0 0021 12.79z",
    bell: "M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9",
    bank: "M3 21h18M3 10h18M3 7l9-4 9 4M4 10h2v9H4v-9zm7 0h2v9h-2v-9zm7 0h2v9h-2v-9z",
    edit: "M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z",
    plus: "M12 5v14M5 12h14",
    trending: "M22 7l-8.5 8.5-5-5L2 17",
    clock: "M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z",
    sms: "M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z",
    star: "M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z",
    close: "M6 18L18 6M6 6l12 12",
    download: "M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M9 19l3 3m0 0l3-3m-3 3V10",
    shield: "M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z",
  };

  return (
    <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="1.8" strokeLinecap="round" strokeLinejoin="round">
      <path d={paths[name] || ""} />
    </svg>
  );
};

// ─── Bottom Nav ──────────────────────────────────────────────────────────────
const BottomNav = ({ active, onNav, dark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const tabs = [
    { id: "home", icon: "home", label: "Home" },
    { id: "transactions", icon: "transactions", label: "Spend" },
    { id: "tax", icon: "tax", label: "Tax" },
    { id: "insights", icon: "insights", label: "Insights" },
    { id: "settings", icon: "profile", label: "Profile" },
  ];

  return (
    <div style={{
      display: "flex", borderTop: `1px solid ${c.border}`,
      background: c.surface, padding: "8px 0 4px",
    }}>
      {tabs.map(t => {
        const isActive = active === t.id;
        return (
          <button key={t.id} onClick={() => onNav(t.id)}
            style={{
              flex: 1, display: "flex", flexDirection: "column", alignItems: "center",
              gap: 3, background: "none", border: "none", cursor: "pointer",
              padding: "4px 0", color: isActive ? COLORS.blue : c.muted,
            }}>
            {isActive && (
              <div style={{
                position: "absolute", width: 32, height: 3, borderRadius: 2,
                background: COLORS.blue, marginTop: -8,
              }} />
            )}
            <Icon name={t.icon} size={22} color={isActive ? COLORS.blue : c.muted} />
            <span style={{ fontSize: 10, fontWeight: isActive ? 700 : 400, letterSpacing: 0.3 }}>
              {t.label}
            </span>
          </button>
        );
      })}
    </div>
  );
};

// ─── Status Bar ──────────────────────────────────────────────────────────────
const StatusBar = ({ dark }) => (
  <div style={{
    display: "flex", justifyContent: "space-between", alignItems: "center",
    padding: "12px 20px 6px", fontSize: 12, fontWeight: 600,
    color: dark ? COLORS.dark.text : COLORS.light.text,
  }}>
    <span>9:41</span>
    <div style={{ display: "flex", gap: 5, alignItems: "center" }}>
      <span style={{ fontSize: 11 }}>●●●●</span>
      <span>WiFi</span>
      <span>100%</span>
    </div>
  </div>
);

// ─── SCREEN 1: Onboarding ────────────────────────────────────────────────────
const OnboardingScreen = ({ dark, onFinish }) => {
  const [step, setStep] = useState(0);
  const [answers, setAnswers] = useState({ type: null, income: null, tax: null });
  const c = dark ? COLORS.dark : COLORS.light;

  const steps = [
    {
      title: "What's your hustle?",
      subtitle: "We'll tailor everything to your business type",
      key: "type",
      options: [
        { value: "freelance", label: "Freelancer", emoji: "💻", sub: "Design, dev, writing" },
        { value: "creative", label: "Creative", emoji: "🎨", sub: "Art, music, content" },
        { value: "trades", label: "Trades", emoji: "🔧", sub: "Plumbing, electrical" },
        { value: "retail", label: "Retail / Resell", emoji: "🛍️", sub: "Products & goods" },
        { value: "food", label: "Food & Bev", emoji: "🍕", sub: "Catering, baking" },
        { value: "other", label: "Other", emoji: "✨", sub: "Something else" },
      ],
    },
    {
      title: "Monthly income range?",
      subtitle: "Helps us estimate your provisional tax",
      key: "income",
      options: [
        { value: "0-5k", label: "Under R5,000", emoji: "🌱" },
        { value: "5-15k", label: "R5k – R15k", emoji: "📈" },
        { value: "15-30k", label: "R15k – R30k", emoji: "💼" },
        { value: "30-60k", label: "R30k – R60k", emoji: "🚀" },
        { value: "60k+", label: "R60k+", emoji: "🏆" },
      ],
    },
    {
      title: "Tax filing status?",
      subtitle: "Your current SARS situation",
      key: "tax",
      options: [
        { value: "registered", label: "Registered for tax", emoji: "✅", sub: "I have a tax number" },
        { value: "provisional", label: "Provisional taxpayer", emoji: "📋", sub: "I file twice a year" },
        { value: "unregistered", label: "Not yet registered", emoji: "🆕", sub: "Help me get started" },
        { value: "unsure", label: "Not sure", emoji: "🤔", sub: "Guide me" },
      ],
    },
  ];

  const current = steps[step];
  const progress = ((step) / steps.length) * 100;
  const nextProgress = ((step + 1) / steps.length) * 100;

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%", background: c.bg }}>
      <StatusBar dark={dark} />

      {/* Header */}
      <div style={{ padding: "8px 24px 0" }}>
        <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 20 }}>
          <div style={{
            width: 32, height: 32, borderRadius: 10,
            background: `linear-gradient(135deg, ${COLORS.blue}, ${COLORS.green})`,
            display: "flex", alignItems: "center", justifyContent: "center",
            fontSize: 16,
          }}>💰</div>
          <span style={{ fontFamily: "'Georgia', serif", fontWeight: 700, fontSize: 16, color: c.text }}>
            SideHustle SA
          </span>
        </div>

        {/* Progress bar */}
        <div style={{ marginBottom: 4 }}>
          <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 8 }}>
            <span style={{ fontSize: 12, color: c.muted }}>Step {step + 1} of {steps.length}</span>
            <span style={{ fontSize: 12, color: COLORS.blue, fontWeight: 600 }}>{Math.round(nextProgress)}%</span>
          </div>
          <div style={{ height: 4, background: c.subtle, borderRadius: 4, overflow: "hidden" }}>
            <div style={{
              height: "100%", borderRadius: 4,
              background: `linear-gradient(90deg, ${COLORS.blue}, ${COLORS.green})`,
              width: `${nextProgress}%`, transition: "width 0.5s ease",
            }} />
          </div>
        </div>
      </div>

      {/* Content */}
      <div style={{ flex: 1, overflowY: "auto", padding: "20px 24px" }}>
        <h2 style={{
          fontFamily: "'Georgia', serif", fontSize: 24, fontWeight: 700,
          color: c.text, marginBottom: 6, lineHeight: 1.2,
        }}>{current.title}</h2>
        <p style={{ color: c.muted, fontSize: 14, marginBottom: 24 }}>{current.subtitle}</p>

        <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
          {current.options.map(opt => {
            const selected = answers[current.key] === opt.value;
            return (
              <button key={opt.value}
                onClick={() => setAnswers(a => ({ ...a, [current.key]: opt.value }))}
                style={{
                  display: "flex", alignItems: "center", gap: 14,
                  padding: "14px 16px", borderRadius: 14, cursor: "pointer",
                  border: `2px solid ${selected ? COLORS.blue : c.border}`,
                  background: selected ? (dark ? `${COLORS.blue}22` : `${COLORS.blue}0f`) : c.card,
                  transition: "all 0.2s", textAlign: "left",
                }}>
                <span style={{ fontSize: 24 }}>{opt.emoji}</span>
                <div style={{ flex: 1 }}>
                  <div style={{ fontSize: 15, fontWeight: 600, color: c.text }}>{opt.label}</div>
                  {opt.sub && <div style={{ fontSize: 12, color: c.muted, marginTop: 1 }}>{opt.sub}</div>}
                </div>
                {selected && (
                  <div style={{
                    width: 22, height: 22, borderRadius: "50%",
                    background: COLORS.blue, display: "flex", alignItems: "center", justifyContent: "center",
                  }}>
                    <Icon name="check" size={13} color="white" />
                  </div>
                )}
              </button>
            );
          })}
        </div>
      </div>

      {/* CTA */}
      <div style={{ padding: "12px 24px 20px" }}>
        <button
          onClick={() => {
            if (!answers[current.key]) return;
            if (step < 2) setStep(s => s + 1);
            else onFinish();
          }}
          style={{
            width: "100%", padding: "16px", borderRadius: 14, border: "none",
            background: answers[current.key]
              ? `linear-gradient(135deg, ${COLORS.blue}, ${COLORS.green})`
              : c.subtle,
            color: answers[current.key] ? "white" : c.muted,
            fontSize: 15, fontWeight: 700, cursor: answers[current.key] ? "pointer" : "not-allowed",
            letterSpacing: 0.3, transition: "all 0.2s",
          }}>
          {step < 2 ? "Continue →" : "Let's go 🚀"}
        </button>
      </div>
    </div>
  );
};

// ─── SCREEN 2: Dashboard ─────────────────────────────────────────────────────
const DashboardScreen = ({ dark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const health = 74;
  const circumference = 2 * Math.PI * 36;

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%", background: c.bg, overflowY: "auto" }}>
      <StatusBar dark={dark} />

      {/* Header */}
      <div style={{
        padding: "8px 20px 20px",
        background: `linear-gradient(160deg, ${COLORS.blue}ee, ${COLORS.green}cc)`,
        borderRadius: "0 0 28px 28px",
      }}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 20 }}>
          <div>
            <p style={{ color: "rgba(255,255,255,0.75)", fontSize: 13, marginBottom: 3 }}>Good morning 👋</p>
            <h2 style={{ color: "white", fontSize: 20, fontWeight: 700, fontFamily: "'Georgia', serif" }}>Thandi M.</h2>
          </div>
          <div style={{
            width: 40, height: 40, borderRadius: "50%",
            background: "rgba(255,255,255,0.2)", display: "flex", alignItems: "center", justifyContent: "center",
          }}>
            <Icon name="bell" size={20} color="white" />
          </div>
        </div>

        {/* Main income card */}
        <div style={{
          background: "rgba(255,255,255,0.15)", backdropFilter: "blur(10px)",
          borderRadius: 20, padding: "18px 20px", border: "1px solid rgba(255,255,255,0.2)",
        }}>
          <p style={{ color: "rgba(255,255,255,0.75)", fontSize: 12, letterSpacing: 1, textTransform: "uppercase", marginBottom: 4 }}>
            June Income
          </p>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-end" }}>
            <div>
              <p style={{ color: "white", fontSize: 32, fontWeight: 800, letterSpacing: -1, lineHeight: 1 }}>
                R14,250
              </p>
              <p style={{ color: "rgba(255,255,255,0.7)", fontSize: 12, marginTop: 4 }}>
                ↑ 12% vs last month
              </p>
            </div>
            <div style={{ textAlign: "right" }}>
              <p style={{ color: "rgba(255,255,255,0.75)", fontSize: 11 }}>Tax set-aside</p>
              <p style={{ color: "#fff", fontSize: 20, fontWeight: 700 }}>R3,990</p>
              <p style={{ color: "rgba(255,255,255,0.6)", fontSize: 10 }}>28% est. rate</p>
            </div>
          </div>
        </div>
      </div>

      <div style={{ padding: "20px 20px 0" }}>
        {/* Health Score + Forecast row */}
        <div style={{ display: "flex", gap: 12, marginBottom: 16 }}>
          {/* Health Score */}
          <div style={{
            flex: 1, background: c.card, borderRadius: 18, padding: "16px",
            border: `1px solid ${c.border}`, display: "flex", flexDirection: "column", alignItems: "center",
          }}>
            <p style={{ fontSize: 11, color: c.muted, marginBottom: 10, letterSpacing: 0.5 }}>HEALTH SCORE</p>
            <svg width={90} height={90} viewBox="0 0 90 90">
              <circle cx={45} cy={45} r={36} fill="none" stroke={c.subtle} strokeWidth={7} />
              <circle cx={45} cy={45} r={36} fill="none"
                stroke={COLORS.green} strokeWidth={7} strokeLinecap="round"
                strokeDasharray={circumference}
                strokeDashoffset={circumference - (health / 100) * circumference}
                transform="rotate(-90 45 45)"
                style={{ transition: "stroke-dashoffset 1s ease" }}
              />
              <text x={45} y={45} textAnchor="middle" dominantBaseline="middle"
                fill={c.text} fontSize={22} fontWeight={800}>{health}</text>
              <text x={45} y={62} textAnchor="middle" fill={c.muted} fontSize={9}>/ 100</text>
            </svg>
            <p style={{ fontSize: 12, color: COLORS.green, fontWeight: 600, marginTop: 6 }}>Good Shape ✓</p>
          </div>

          {/* Forecast */}
          <div style={{ flex: 1, display: "flex", flexDirection: "column", gap: 10 }}>
            {[
              { month: "Jun", status: "green", label: "On Track", amount: "R14.2k" },
              { month: "Jul", status: "yellow", label: "Watch Out", amount: "R9.8k" },
              { month: "Aug", status: "red", label: "Lean Month", amount: "R6.1k" },
            ].map(row => (
              <div key={row.month} style={{
                background: c.card, borderRadius: 12, padding: "10px 14px",
                border: `1px solid ${c.border}`, display: "flex", alignItems: "center", gap: 10,
              }}>
                <div style={{
                  width: 10, height: 10, borderRadius: "50%", flexShrink: 0,
                  background: row.status === "green" ? COLORS.green : row.status === "yellow" ? COLORS.yellow : COLORS.red,
                  boxShadow: `0 0 6px ${row.status === "green" ? COLORS.green : row.status === "yellow" ? COLORS.yellow : COLORS.red}80`,
                }} />
                <div style={{ flex: 1 }}>
                  <p style={{ fontSize: 11, color: c.muted }}>{row.month}</p>
                  <p style={{ fontSize: 12, fontWeight: 700, color: c.text }}>{row.label}</p>
                </div>
                <span style={{ fontSize: 13, fontWeight: 700, color: c.text }}>{row.amount}</span>
              </div>
            ))}
          </div>
        </div>

        {/* Quick Actions */}
        <div style={{ background: c.card, borderRadius: 18, padding: "16px", border: `1px solid ${c.border}`, marginBottom: 16 }}>
          <p style={{ fontSize: 13, fontWeight: 700, color: c.text, marginBottom: 14 }}>Quick Actions</p>
          <div style={{ display: "flex", justifyContent: "space-around" }}>
            {[
              { icon: "plus", label: "Add Income", color: COLORS.green },
              { icon: "tax", label: "Tax Check", color: COLORS.blue },
              { icon: "insights", label: "Insights", color: "#9b59b6" },
              { icon: "bank", label: "Link Bank", color: COLORS.yellow },
            ].map(a => (
              <div key={a.label} style={{ display: "flex", flexDirection: "column", alignItems: "center", gap: 7, cursor: "pointer" }}>
                <div style={{
                  width: 46, height: 46, borderRadius: 14,
                  background: `${a.color}22`, display: "flex", alignItems: "center", justifyContent: "center",
                  border: `1px solid ${a.color}44`,
                }}>
                  <Icon name={a.icon} size={20} color={a.color} />
                </div>
                <span style={{ fontSize: 10, color: c.muted, textAlign: "center" }}>{a.label}</span>
              </div>
            ))}
          </div>
        </div>

        {/* Recent */}
        <div style={{ background: c.card, borderRadius: 18, padding: "16px", border: `1px solid ${c.border}`, marginBottom: 16 }}>
          <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 14 }}>
            <p style={{ fontSize: 13, fontWeight: 700, color: c.text }}>Recent Transactions</p>
            <span style={{ fontSize: 12, color: COLORS.blue, fontWeight: 600 }}>See all</span>
          </div>
          {[
            { name: "Upwork Payment", cat: "Freelance", amount: "+R4,800", time: "2h ago", pos: true },
            { name: "Adobe CC", cat: "Software", amount: "-R289", time: "Yesterday", pos: false },
          ].map((t, i) => (
            <div key={i} style={{
              display: "flex", alignItems: "center", gap: 12,
              paddingBottom: i === 0 ? 12 : 0, borderBottom: i === 0 ? `1px solid ${c.border}` : "none",
              paddingTop: i === 1 ? 12 : 0,
            }}>
              <div style={{
                width: 40, height: 40, borderRadius: 12,
                background: t.pos ? `${COLORS.green}22` : `${COLORS.red}22`,
                display: "flex", alignItems: "center", justifyContent: "center",
                fontSize: 18,
              }}>
                {t.pos ? "💸" : "📦"}
              </div>
              <div style={{ flex: 1 }}>
                <p style={{ fontSize: 13, fontWeight: 600, color: c.text }}>{t.name}</p>
                <p style={{ fontSize: 11, color: c.muted }}>{t.cat} · {t.time}</p>
              </div>
              <span style={{ fontSize: 14, fontWeight: 700, color: t.pos ? COLORS.green : COLORS.red }}>
                {t.amount}
              </span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// ─── SCREEN 3: Transactions ──────────────────────────────────────────────────
const TransactionsScreen = ({ dark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const [smsToggle, setSmsToggle] = useState(true);
  const [filter, setFilter] = useState("all");

  const txs = [
    { id: 1, name: "Fiverr Payout", cat: "Freelance", amount: 3200, date: "Jun 3", pos: true, auto: true, emoji: "💻" },
    { id: 2, name: "Canva Pro", cat: "Software", amount: -189, date: "Jun 3", pos: false, auto: true, emoji: "🎨" },
    { id: 3, name: "Client Retainer — MTN", cat: "Freelance", amount: 7500, date: "Jun 2", pos: true, auto: false, emoji: "📱" },
    { id: 4, name: "Takealot Shipping", cat: "Logistics", amount: -94, date: "Jun 2", pos: false, auto: true, emoji: "📦" },
    { id: 5, name: "EFT — Design Invoice", cat: "Design", amount: 2800, date: "Jun 1", pos: true, auto: false, emoji: "✏️" },
    { id: 6, name: "Uber Eats", cat: "Meals", amount: -156, date: "Jun 1", pos: false, auto: true, emoji: "🍔" },
  ];

  const filters = ["all", "income", "expenses"];
  const filtered = filter === "all" ? txs : filter === "income" ? txs.filter(t => t.pos) : txs.filter(t => !t.pos);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%", background: c.bg }}>
      <StatusBar dark={dark} />

      {/* Header */}
      <div style={{ padding: "4px 20px 16px" }}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 16 }}>
          <h2 style={{ fontFamily: "'Georgia', serif", fontSize: 22, fontWeight: 700, color: c.text }}>Transactions</h2>
          <div style={{ display: "flex", gap: 10 }}>
            {/* SMS Toggle */}
            <div style={{
              display: "flex", alignItems: "center", gap: 6,
              background: c.card, borderRadius: 20, padding: "6px 12px",
              border: `1px solid ${c.border}`, cursor: "pointer",
            }}
              onClick={() => setSmsToggle(s => !s)}>
              <Icon name="sms" size={14} color={smsToggle ? COLORS.green : c.muted} />
              <span style={{ fontSize: 11, color: smsToggle ? COLORS.green : c.muted, fontWeight: 600 }}>
                SMS Parse {smsToggle ? "ON" : "OFF"}
              </span>
              <div style={{
                width: 28, height: 16, borderRadius: 8,
                background: smsToggle ? COLORS.green : c.subtle,
                position: "relative", transition: "background 0.2s",
              }}>
                <div style={{
                  width: 12, height: 12, borderRadius: "50%", background: "white",
                  position: "absolute", top: 2,
                  left: smsToggle ? 14 : 2, transition: "left 0.2s",
                }} />
              </div>
            </div>
          </div>
        </div>

        {/* Summary bar */}
        <div style={{
          background: `linear-gradient(135deg, ${COLORS.blue}22, ${COLORS.green}22)`,
          borderRadius: 14, padding: "12px 16px", marginBottom: 16,
          border: `1px solid ${COLORS.blue}33`, display: "flex", justifyContent: "space-between",
        }}>
          <div style={{ textAlign: "center" }}>
            <p style={{ fontSize: 11, color: c.muted }}>Income</p>
            <p style={{ fontSize: 16, fontWeight: 800, color: COLORS.green }}>+R13,500</p>
          </div>
          <div style={{ width: 1, background: c.border }} />
          <div style={{ textAlign: "center" }}>
            <p style={{ fontSize: 11, color: c.muted }}>Expenses</p>
            <p style={{ fontSize: 16, fontWeight: 800, color: COLORS.red }}>-R439</p>
          </div>
          <div style={{ width: 1, background: c.border }} />
          <div style={{ textAlign: "center" }}>
            <p style={{ fontSize: 11, color: c.muted }}>Net</p>
            <p style={{ fontSize: 16, fontWeight: 800, color: c.text }}>R13,061</p>
          </div>
        </div>

        {/* Filters */}
        <div style={{ display: "flex", gap: 8 }}>
          {filters.map(f => (
            <button key={f} onClick={() => setFilter(f)}
              style={{
                padding: "7px 16px", borderRadius: 20, border: "none", cursor: "pointer",
                background: filter === f ? COLORS.blue : c.subtle,
                color: filter === f ? "white" : c.muted,
                fontSize: 12, fontWeight: 600, textTransform: "capitalize",
              }}>
              {f}
            </button>
          ))}
        </div>
      </div>

      {/* List */}
      <div style={{ flex: 1, overflowY: "auto", padding: "0 20px" }}>
        {filtered.map((t, i) => (
          <div key={t.id} style={{
            display: "flex", alignItems: "center", gap: 12,
            padding: "12px 0", borderBottom: `1px solid ${c.border}`,
          }}>
            <div style={{
              width: 44, height: 44, borderRadius: 14,
              background: t.pos ? `${COLORS.green}18` : `${COLORS.red}18`,
              display: "flex", alignItems: "center", justifyContent: "center", fontSize: 20,
            }}>
              {t.emoji}
            </div>
            <div style={{ flex: 1 }}>
              <p style={{ fontSize: 13, fontWeight: 600, color: c.text, marginBottom: 2 }}>{t.name}</p>
              <div style={{ display: "flex", gap: 6, alignItems: "center" }}>
                <span style={{
                  fontSize: 10, padding: "2px 8px", borderRadius: 6, fontWeight: 600,
                  background: COLORS.blue + "22", color: COLORS.blue,
                }}>{t.cat}</span>
                {t.auto && <span style={{ fontSize: 10, color: c.muted }}>● Auto-detected</span>}
                <span style={{ fontSize: 10, color: c.muted }}>{t.date}</span>
              </div>
            </div>
            <div style={{ display: "flex", flexDirection: "column", alignItems: "flex-end", gap: 4 }}>
              <span style={{ fontSize: 14, fontWeight: 700, color: t.pos ? COLORS.green : COLORS.red }}>
                {t.pos ? "+" : ""}R{Math.abs(t.amount).toLocaleString()}
              </span>
              <button style={{
                background: "none", border: "none", cursor: "pointer", padding: 2,
              }}>
                <Icon name="edit" size={14} color={c.muted} />
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

// ─── SCREEN 4: Tax Center ────────────────────────────────────────────────────
const TaxScreen = ({ dark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const daysLeft = 47;
  const totalCirc = 2 * Math.PI * 30;
  const savingsGoal = 12000;
  const saved = 7800;
  const pct = saved / savingsGoal;

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%", background: c.bg, overflowY: "auto" }}>
      <StatusBar dark={dark} />
      <div style={{ padding: "4px 20px 20px" }}>
        <h2 style={{ fontFamily: "'Georgia', serif", fontSize: 22, fontWeight: 700, color: c.text, marginBottom: 4 }}>Tax Centre</h2>
        <p style={{ fontSize: 13, color: c.muted, marginBottom: 20 }}>Provisional Tax · 2025/26</p>

        {/* Deadline Countdown */}
        <div style={{
          background: `linear-gradient(135deg, ${dark ? "#1a0a0a" : "#fff5f5"}, ${dark ? "#0a1a0a" : "#f0fff8"})`,
          borderRadius: 20, padding: "20px", marginBottom: 14,
          border: `1px solid ${daysLeft < 30 ? COLORS.red + "66" : COLORS.yellow + "66"}`,
          display: "flex", alignItems: "center", gap: 16,
        }}>
          <div style={{ position: "relative" }}>
            <svg width={72} height={72} viewBox="0 0 72 72">
              <circle cx={36} cy={36} r={30} fill="none" stroke={c.subtle} strokeWidth={6} />
              <circle cx={36} cy={36} r={30} fill="none"
                stroke={daysLeft < 30 ? COLORS.red : COLORS.yellow}
                strokeWidth={6} strokeLinecap="round"
                strokeDasharray={totalCirc}
                strokeDashoffset={totalCirc * (1 - daysLeft / 180)}
                transform="rotate(-90 36 36)"
              />
              <text x={36} y={34} textAnchor="middle" fill={c.text} fontSize={18} fontWeight={800}>{daysLeft}</text>
              <text x={36} y={48} textAnchor="middle" fill={c.muted} fontSize={8}>days</text>
            </svg>
          </div>
          <div style={{ flex: 1 }}>
            <p style={{ fontSize: 12, color: c.muted, marginBottom: 4 }}>Next SARS Deadline</p>
            <p style={{ fontSize: 16, fontWeight: 700, color: c.text }}>1st Provisional</p>
            <p style={{ fontSize: 13, color: daysLeft < 30 ? COLORS.red : COLORS.yellow, fontWeight: 600 }}>
              Due 31 July 2025 ⚠️
            </p>
          </div>
        </div>

        {/* Tax Calculator */}
        <div style={{
          background: c.card, borderRadius: 20, padding: "18px", marginBottom: 14,
          border: `1px solid ${c.border}`,
        }}>
          <p style={{ fontSize: 14, fontWeight: 700, color: c.text, marginBottom: 16 }}>Tax Estimate</p>
          {[
            { label: "Estimated Annual Income", value: "R171,000", note: "Based on Q1" },
            { label: "Tax Threshold (2026)", value: "R95,750", note: "SARS standard" },
            { label: "Taxable Income", value: "R75,250", note: "Above threshold" },
            { label: "Tax Rate", value: "18%", note: "First bracket" },
            { label: "Provisional Tax Due", value: "R13,545", note: "Split into 2", bold: true },
            { label: "Each Payment", value: "R6,772", note: "Per period", highlight: true },
          ].map((row, i) => (
            <div key={i} style={{
              display: "flex", justifyContent: "space-between", alignItems: "center",
              paddingBottom: 10, marginBottom: 10,
              borderBottom: i < 5 ? `1px solid ${c.border}` : "none",
            }}>
              <div>
                <p style={{ fontSize: 13, color: row.bold ? c.text : c.muted, fontWeight: row.bold ? 700 : 400 }}>
                  {row.label}
                </p>
                <p style={{ fontSize: 10, color: c.muted }}>{row.note}</p>
              </div>
              <span style={{
                fontSize: row.highlight ? 18 : 14,
                fontWeight: row.highlight || row.bold ? 800 : 600,
                color: row.highlight ? COLORS.blue : c.text,
              }}>
                {row.value}
              </span>
            </div>
          ))}
        </div>

        {/* Savings Progress */}
        <div style={{
          background: c.card, borderRadius: 20, padding: "18px", marginBottom: 14,
          border: `1px solid ${c.border}`,
        }}>
          <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 12 }}>
            <p style={{ fontSize: 14, fontWeight: 700, color: c.text }}>Tax Savings Goal</p>
            <span style={{ fontSize: 13, color: COLORS.green, fontWeight: 700 }}>
              {Math.round(pct * 100)}%
            </span>
          </div>
          <div style={{ height: 10, background: c.subtle, borderRadius: 6, overflow: "hidden", marginBottom: 8 }}>
            <div style={{
              height: "100%", borderRadius: 6,
              background: `linear-gradient(90deg, ${COLORS.blue}, ${COLORS.green})`,
              width: `${pct * 100}%`, transition: "width 1s ease",
            }} />
          </div>
          <div style={{ display: "flex", justifyContent: "space-between" }}>
            <span style={{ fontSize: 12, color: COLORS.green, fontWeight: 600 }}>R7,800 saved</span>
            <span style={{ fontSize: 12, color: c.muted }}>Goal: R12,000</span>
          </div>
          <p style={{ fontSize: 12, color: c.muted, marginTop: 8 }}>
            💡 Set aside <strong style={{ color: COLORS.blue }}>R1,050/month</strong> for 4 months to hit goal
          </p>
        </div>

        {/* Pay Now CTA */}
        <button style={{
          width: "100%", padding: "16px", borderRadius: 14, border: "none",
          background: `linear-gradient(135deg, ${COLORS.blue}, ${COLORS.blueDark})`,
          color: "white", fontSize: 15, fontWeight: 700, cursor: "pointer",
          display: "flex", alignItems: "center", justifyContent: "center", gap: 10,
          boxShadow: `0 4px 20px ${COLORS.blue}44`,
          marginBottom: 10,
        }}>
          <Icon name="shield" size={18} color="white" />
          Pay Now via SARS eFiling →
        </button>

        <button style={{
          width: "100%", padding: "14px", borderRadius: 14,
          border: `1px solid ${c.border}`,
          background: "transparent", color: c.muted,
          fontSize: 14, fontWeight: 600, cursor: "pointer",
        }}>
          Download Tax Certificate
        </button>
      </div>
    </div>
  );
};

// ─── SCREEN 5: Insights ──────────────────────────────────────────────────────
const InsightsScreen = ({ dark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const insights = [
    {
      id: 1, urgent: true, emoji: "🔔",
      tag: "Tax Alert", tagColor: COLORS.red,
      title: "Set aside R1,200 more",
      body: "Based on your Q1 income of R42,750, your provisional tax estimate is higher than expected. Consider increasing monthly set-asides.",
      action: "Adjust Goal",
      time: "Today",
      icon: "tax",
    },
    {
      id: 2, urgent: false, emoji: "📈",
      tag: "Income Pattern", tagColor: COLORS.blue,
      title: "Your peak months are Q1",
      body: "You earned 34% more in Jan–Mar compared to other quarters. Consider higher tax set-asides during these months.",
      action: "See Pattern",
      time: "2 days ago",
      icon: "trending",
    },
    {
      id: 3, urgent: false, emoji: "💡",
      tag: "Smart Tip", tagColor: COLORS.green,
      title: "R2,860 deductible this year",
      body: "Your home office and software expenses qualify for deductions. Claiming these could reduce your taxable income significantly.",
      action: "Claim Deductions",
      time: "This week",
      icon: "star",
    },
    {
      id: 4, urgent: false, emoji: "⚠️",
      tag: "Forecast", tagColor: COLORS.yellow,
      title: "July looks lean",
      body: "Based on seasonal patterns and your client pipeline, July income may dip below R8,000. Plan ahead.",
      action: "View Forecast",
      time: "This week",
      icon: "clock",
    },
  ];

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%", background: c.bg }}>
      <StatusBar dark={dark} />
      <div style={{ padding: "4px 20px 16px" }}>
        <h2 style={{ fontFamily: "'Georgia', serif", fontSize: 22, fontWeight: 700, color: c.text }}>Insights</h2>
        <p style={{ fontSize: 13, color: c.muted, marginTop: 2 }}>AI-powered weekly analysis</p>
      </div>

      {/* Weekly score banner */}
      <div style={{
        margin: "0 20px 16px",
        background: `linear-gradient(135deg, ${COLORS.blue}, ${COLORS.green})`,
        borderRadius: 18, padding: "16px 20px",
        display: "flex", alignItems: "center", justifyContent: "space-between",
      }}>
        <div>
          <p style={{ color: "rgba(255,255,255,0.8)", fontSize: 12 }}>Week of Jun 2–8</p>
          <p style={{ color: "white", fontSize: 18, fontWeight: 700 }}>4 new insights</p>
        </div>
        <div style={{
          width: 50, height: 50, borderRadius: "50%",
          background: "rgba(255,255,255,0.2)",
          display: "flex", alignItems: "center", justifyContent: "center",
          fontSize: 24,
        }}>🤖</div>
      </div>

      <div style={{ flex: 1, overflowY: "auto", padding: "0 20px" }}>
        {insights.map((ins, i) => (
          <div key={ins.id} style={{
            background: c.card, borderRadius: 18, padding: "16px", marginBottom: 12,
            border: `1px solid ${ins.urgent ? ins.tagColor + "44" : c.border}`,
            boxShadow: ins.urgent ? `0 0 0 1px ${ins.tagColor}33` : "none",
          }}>
            <div style={{ display: "flex", alignItems: "flex-start", gap: 12 }}>
              <div style={{
                width: 44, height: 44, borderRadius: 13,
                background: `${ins.tagColor}22`,
                display: "flex", alignItems: "center", justifyContent: "center", fontSize: 22,
                flexShrink: 0,
              }}>
                {ins.emoji}
              </div>
              <div style={{ flex: 1 }}>
                <div style={{ display: "flex", gap: 8, marginBottom: 6, alignItems: "center" }}>
                  <span style={{
                    fontSize: 10, padding: "2px 8px", borderRadius: 6, fontWeight: 700,
                    background: `${ins.tagColor}22`, color: ins.tagColor, letterSpacing: 0.3,
                  }}>{ins.tag}</span>
                  <span style={{ fontSize: 10, color: c.muted }}>{ins.time}</span>
                  {ins.urgent && <span style={{ fontSize: 10, color: COLORS.red, fontWeight: 700 }}>● Urgent</span>}
                </div>
                <p style={{ fontSize: 14, fontWeight: 700, color: c.text, marginBottom: 6 }}>{ins.title}</p>
                <p style={{ fontSize: 12, color: c.muted, lineHeight: 1.5, marginBottom: 12 }}>{ins.body}</p>
                <button style={{
                  padding: "8px 14px", borderRadius: 10, border: "none",
                  background: `${ins.tagColor}22`, color: ins.tagColor,
                  fontSize: 12, fontWeight: 700, cursor: "pointer",
                }}>
                  {ins.action} →
                </button>
              </div>
            </div>
          </div>
        ))}
        <div style={{ height: 10 }} />
      </div>
    </div>
  );
};

// ─── SCREEN 6: Settings ──────────────────────────────────────────────────────
const SettingsScreen = ({ dark, setDark }) => {
  const c = dark ? COLORS.dark : COLORS.light;
  const [notifs, setNotifs] = useState({ deadlines: true, weekly: true, lowCash: false, taxTips: true });
  const [plan, setPlan] = useState("pro");

  const Toggle = ({ value, onChange }) => (
    <div style={{
      width: 44, height: 24, borderRadius: 12,
      background: value ? COLORS.green : c.subtle,
      position: "relative", cursor: "pointer", transition: "background 0.2s",
    }}
      onClick={() => onChange(!value)}>
      <div style={{
        width: 18, height: 18, borderRadius: "50%", background: "white",
          }}>T</div>
          <div style={{ flex: 1 }}>
            <p style={{ fontSize: 16, fontWeight: 700, color: c.text }}>Thandi Mokoena</p>
            <p style={{ fontSize: 12, color: c.muted }}>thandi@freelance.co.za</p>
            <span style={{
              fontSize: 10, padding: "2px 8px", borderRadius: 6, fontWeight: 700,
              background: `${COLORS.green}22`, color: COLORS.green, marginTop: 4, display: "inline-block",
            }}>Pro Plan ✓</span>
          </div>
          <Icon name="edit" size={18} color={c.muted} />
        </div>

        {/* Dark mode */}
        <div style={{ background: c.card, borderRadius: 18, padding: "6px 16px", marginBottom: 14, border: `1px solid ${c.border}` }}>
          <div style={{
            display: "flex", justifyContent: "space-between", alignItems: "center", padding: "12px 0",
            borderBottom: `1px solid ${c.border}`,
          }}>
            <div style={{ display: "flex", gap: 10, alignItems: "center" }}>
              <Icon name={dark ? "moon" : "sun"} size={18} color={dark ? COLORS.blue : COLORS.yellow} />
              <span style={{ fontSize: 14, color: c.text, fontWeight: 500 }}>Dark Mode</span>
            </div>
            <Toggle value={dark} onChange={setDark} />
          </div>
        </div>

        {/* Bank accounts */}
        <div style={{ background: c.card, borderRadius: 18, padding: "6px 16px", marginBottom: 14, border: `1px solid ${c.border}` }}>
          <p style={{ fontSize: 12, fontWeight: 700, color: c.muted, letterSpacing: 0.8, textTransform: "uppercase", paddingTop: 8, paddingBottom: 4 }}>Bank Accounts</p>
          {[
            { bank: "FNB Cheque", last4: "7823", linked: true, emoji: "🏦" },
            { bank: "Capitec Savings", last4: "1190", linked: true, emoji: "🏛️" },
          ].map((b, i) => (
            <div key={i} style={{
              display: "flex", alignItems: "center", gap: 12, padding: "12px 0",
              borderBottom: `1px solid ${c.border}`,
            }}>
              <span style={{ fontSize: 22 }}>{b.emoji}</span>
              <div style={{ flex: 1 }}>
                <p style={{ fontSize: 13, fontWeight: 600, color: c.text }}>{b.bank}</p>
                <p style={{ fontSize: 11, color: c.muted }}>••••{b.last4}</p>
              </div>
              <span style={{
                fontSize: 10, padding: "3px 8px", borderRadius: 6, fontWeight: 700,
                background: `${COLORS.green}22`, color: COLORS.green,
              }}>Linked</span>
            </div>
          ))}
          <button style={{
            width: "100%", padding: "12px", background: "none", border: "none",
            color: COLORS.blue, fontSize: 13, fontWeight: 600, cursor: "pointer", textAlign: "left",
            display: "flex", alignItems: "center", gap: 8, marginTop: 4,
          }}>
            <Icon name="plus" size={16} color={COLORS.blue} />
            Add another account
          </button>
        </div>

        {/* Notifications */}
        <div style={{ background: c.card, borderRadius: 18, padding: "6px 16px", marginBottom: 14, border: `1px solid ${c.border}` }}>
          <p style={{ fontSize: 12, fontWeight: 700, color: c.muted, letterSpacing: 0.8, textTransform: "uppercase", paddingTop: 8, paddingBottom: 4 }}>Notifications</p>
          {[
            { key: "deadlines", label: "SARS Deadlines", sub: "Payment & filing reminders" },
            { key: "weekly", label: "Weekly Insights", sub: "AI-generated summary" },
            { key: "lowCash", label: "Low Cash Warning", sub: "When forecast dips" },
            { key: "taxTips", label: "Tax-saving Tips", sub: "Monthly deduction tips" },
          ].map((n, i) => (
            <div key={n.key} style={{
              display: "flex", justifyContent: "space-between", alignItems: "center",
              padding: "12px 0", borderBottom: i < 3 ? `1px solid ${c.border}` : "none",
            }}>
              <div>
                <p style={{ fontSize: 13, fontWeight: 600, color: c.text }}>{n.label}</p>
                <p style={{ fontSize: 11, color: c.muted }}>{n.sub}</p>
              </div>
              <Toggle value={notifs[n.key]} onChange={v => setNotifs(ns => ({ ...ns, [n.key]: v }))} />
            </div>
          ))}
        </div>

        {/* Subscription */}
        <div style={{
          background: `linear-gradient(135deg, ${COLORS.blue}15, ${COLORS.green}15)`,
          borderRadius: 18, padding: "16px", marginBottom: 14,
          border: `1px solid ${COLORS.blue}33`,
        }}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 10 }}>
            <p style={{ fontSize: 14, fontWeight: 700, color: c.text }}>Subscription</p>
            <span style={{
              fontSize: 10, padding: "3px 10px", borderRadius: 6, fontWeight: 700,
              background: COLORS.blue, color: "white",
            }}>PRO</span>
          </div>
          {[
            { label: "Plan", value: "SideHustle Pro" },
            { label: "Billing", value: "R99/month" },
            { label: "Renews", value: "Jul 3, 2025" },
          ].map((r, i) => (
            <div key={i} style={{
              display: "flex", justifyContent: "space-between",
              paddingBottom: 6, marginBottom: 6,
              borderBottom: i < 2 ? `1px solid ${COLORS.blue}22` : "none",
            }}>
              <span style={{ fontSize: 12, color: c.muted }}>{r.label}</span>
              <span style={{ fontSize: 12, fontWeight: 600, color: c.text }}>{r.value}</span>
            </div>
          ))}
          <button style={{
            width: "100%", padding: "10px", marginTop: 8, borderRadius: 10, border: "none",
            background: `linear-gradient(135deg, ${COLORS.blue}, ${COLORS.green})`,
            color: "white", fontSize: 13, fontWeight: 700, cursor: "pointer",
          }}>
            Manage Subscription
          </button>
        </div>

        <div style={{ height: 20 }} />
      </div>
    </div>
  );
};

// ─── MAIN APP ────────────────────────────────────────────────────────────────
export default function App() {
  const [dark, setDark] = useState(false);
  const [screen, setScreen] = useState("onboarding");
  const [activeTab, setActiveTab] = useState("home");
  const c = dark ? COLORS.dark : COLORS.light;

  const handleNav = (tab) => {
    setActiveTab(tab);
    setScreen(tab === "home" ? "home" : tab);
  };

  const renderScreen = () => {
    if (screen === "onboarding") return <OnboardingScreen dark={dark} onFinish={() => setScreen("home")} />;
    if (screen === "home") return <DashboardScreen dark={dark} />;
    if (screen === "transactions") return <TransactionsScreen dark={dark} />;
    if (screen === "tax") return <TaxScreen dark={dark} />;
    if (screen === "insights") return <InsightsScreen dark={dark} />;
    if (screen === "settings") return <SettingsScreen dark={dark} setDark={setDark} />;
    return <DashboardScreen dark={dark} />;
  };

  const showNav = screen !== "onboarding";

  return (
    <div style={{
      minHeight: "100vh", background: dark ? "#0a0e14" : "#e8edf2",
      display: "flex", alignItems: "center", justifyContent: "center",
      fontFamily: "'DM Sans', -apple-system, sans-serif",
      padding: "20px 16px",
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&family=Lora:wght@600;700&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        ::-webkit-scrollbar { width: 0; }
        button { font-family: 'DM Sans', sans-serif; }
      `}</style>

      {/* Multi-phone layout */}
      <div style={{
        display: "flex", gap: 24, flexWrap: "wrap", justifyContent: "center", alignItems: "flex-start",
        maxWidth: 1400,
      }}>
        {/* Phone shell - shows selected screen */}
        <div>
          <p style={{ color: dark ? "#888" : "#666", fontSize: 12, textAlign: "center", marginBottom: 12, fontWeight: 600, letterSpacing: 1 }}>
            INTERACTIVE PROTOTYPE
          </p>
          <div style={{
            width: 375, height: 750,
            background: c.surface, borderRadius: 44,
            boxShadow: dark
              ? `0 0 0 1px #333, 0 30px 80px rgba(0,0,0,0.8), inset 0 0 0 1px #222`
              : `0 0 0 1px #ccc, 0 30px 80px rgba(0,0,0,0.2), inset 0 0 0 1px #f0f0f0`,
            overflow: "hidden", display: "flex", flexDirection: "column",
            position: "relative",
          }}>
            {/* Notch */}
            <div style={{
              position: "absolute", top: 0, left: "50%", transform: "translateX(-50%)",
              width: 120, height: 30, background: dark ? "#0d1117" : "#f8f8f8",
              borderRadius: "0 0 20px 20px", zIndex: 10,
              boxShadow: dark ? "inset 0 -2px 8px rgba(0,0,0,0.5)" : "inset 0 -2px 4px rgba(0,0,0,0.08)",
            }} />

            <div style={{ flex: 1, overflowY: "auto", overflowX: "hidden" }}>
              {renderScreen()}
            </div>

            {showNav && (
              <BottomNav active={activeTab} onNav={handleNav} dark={dark} />
            )}
          </div>

          {/* Nav buttons below phone */}
          {showNav && (
            <div style={{ display: "flex", gap: 8, marginTop: 16, justifyContent: "center", flexWrap: "wrap" }}>
              {[
                { id: "home", label: "Dashboard" },
                { id: "transactions", label: "Transactions" },
                { id: "tax", label: "Tax Centre" },
                { id: "insights", label: "Insights" },
                { id: "settings", label: "Settings" },
              ].map(b => (
                <button key={b.id}
                  onClick={() => handleNav(b.id)}
                  style={{
                    padding: "7px 14px", borderRadius: 20, border: "none", cursor: "pointer",
                    background: activeTab === b.id ? COLORS.blue : dark ? "#1c2330" : "white",
                    color: activeTab === b.id ? "white" : dark ? "#888" : "#444",
                    fontSize: 12, fontWeight: 600,
                    boxShadow: activeTab === b.id ? `0 2px 12px ${COLORS.blue}55` : "none",
                  }}>
                  {b.label}
                </button>
              ))}
            </div>
          )}

          {screen === "onboarding" && (
            <p style={{ color: dark ? "#666" : "#999", fontSize: 11, textAlign: "center", marginTop: 12 }}>
              Complete the wizard to see all screens
            </p>
          )}
        </div>

        {/* Static previews of all screens */}
        {showNav && (
          <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
            <p style={{ color: dark ? "#888" : "#666", fontSize: 12, fontWeight: 600, letterSpacing: 1 }}>
              ALL SCREENS PREVIEW
            </p>
            <div style={{ display: "flex", gap: 16, flexWrap: "wrap" }}>
              {[
                { id: "home", label: "Dashboard", comp: <DashboardScreen dark={dark} /> },
                { id: "transactions", label: "Transactions", comp: <TransactionsScreen dark={dark} /> },
                { id: "tax", label: "Tax Centre", comp: <TaxScreen dark={dark} /> },
                { id: "insights", label: "Insights", comp: <InsightsScreen dark={dark} /> },
                { id: "settings", label: "Settings", comp: <SettingsScreen dark={dark} setDark={setDark} /> },
              ].map(s => (
                <div key={s.id} onClick={() => handleNav(s.id)}
                  style={{ cursor: "pointer" }}>
                  <p style={{
                    color: activeTab === s.id ? COLORS.blue : dark ? "#888" : "#666",
                    fontSize: 11, textAlign: "center", marginBottom: 8, fontWeight: activeTab === s.id ? 700 : 400,
                  }}>{s.label}</p>
                  <div style={{
                    width: 160, height: 320, borderRadius: 24,
                    background: c.surface, overflow: "hidden",
                    boxShadow: activeTab === s.id
                      ? `0 0 0 2px ${COLORS.blue}, 0 12px 40px rgba(0,0,0,0.2)`
                      : dark ? `0 0 0 1px #333` : `0 0 0 1px #ddd`,
                    transform: "scale(0.428)",
                    transformOrigin: "top left",
                    position: "relative",
                  }}>
                    <div style={{ width: 375, height: 750, transform: "none", transformOrigin: "top left" }}>
                      <div style={{ transform: "scale(0.428)", transformOrigin: "top left", width: `${100/0.428}%`, height: `${100/0.428}%` }}>
                        {s.comp}
                      </div>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
}