```jsx
import { useState } from "react";

const steps = [
  { text: "Analysing the request...", icon: "🔬", duration: 1200 },
  { text: "Consulting Elon Musk...", icon: "🚀", duration: 1400 },
  { text: "Searching Epstein files...", icon: "📁", duration: 1600 },
  { text: "Running DNA test...", icon: "🧬", duration: 1300 },
];

const predictions = [
  "Today you will accidentally like a 3-year-old Instagram post and immediately fake your own death.",
  "A pigeon will make direct eye contact with you and you will feel judged.",
  "You'll open the fridge 7 times hoping something new appears. It won't.",
  "Someone will say 'per my last email' to you and you will age 10 years instantly.",
  "You will mishear someone and say 'haha yeah' — it was a question.",
  "Your day will peak at 10:43 AM. You won't know why. You'll never know why.",
  "A text you've been avoiding will be sent to the wrong person. Godspeed.",
  "You will explain something confidently and be completely wrong. Twice.",
  "Mercury is in retrograde which explains everything but fixes nothing.",
  "Today holds great promise. The promise will be broken by noon.",
  "You will step on a Lego. The universe is balanced.",
  "Someone will breathe loudly near you and you will consider moving countries.",
];

const moods = ["💀", "😭", "🤡", "👁️", "💀", "✨", "🫠", "😤", "🌀", "🎭", "⚡", "🔮"];

export default function DayPredictor() {
  const [name, setName] = useState("");
  const [phase, setPhase] = useState("idle");
  const [currentStep, setCurrentStep] = useState(0);
  const [prediction, setPrediction] = useState("");
  const [mood, setMood] = useState("");

  const runPrediction = async () => {
    if (!name.trim()) return;
    setPhase("loading");
    setCurrentStep(0);

    for (let i = 0; i < steps.length; i++) {
      setCurrentStep(i);
      await new Promise((r) => setTimeout(r, steps[i].duration));
    }

    const idx = Math.floor(Math.random() * predictions.length);
    setPrediction(predictions[idx]);
    setMood(moods[idx]);
    setPhase("done");
  };

  const reset = () => {
    setPhase("idle");
    setCurrentStep(0);
    setPrediction("");
    setName("");
  };

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0a0a0f",
      display: "flex",
      alignItems: "center",
      justifyContent: "center",
      fontFamily: "'Courier New', monospace",
      padding: "20px",
      position: "relative",
      overflow: "hidden",
    }}>
      <div style={{
        position: "fixed", inset: 0, zIndex: 0,
        backgroundImage: `linear-gradient(rgba(255,200,0,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(255,200,0,0.03) 1px, transparent 1px)`,
        backgroundSize: "40px 40px",
        animation: "gridScroll 20s linear infinite",
      }} />

      <style>{`
        @keyframes gridScroll { from { background-position: 0 0; } to { background-position: 40px 40px; } }
        @keyframes flicker { 0%,100%{opacity:1} 50%{opacity:0.85} 75%{opacity:0.95} }
        @keyframes pulse { 0%,100%{transform:scale(1)} 50%{transform:scale(1.05)} }
        @keyframes slideUp { from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:translateY(0)} }
        @keyframes scanline { 0%{top:-10%} 100%{top:110%} }
        @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
        @keyframes glow { 0%,100%{text-shadow:0 0 10px #ffd700,0 0 20px #ffd700} 50%{text-shadow:0 0 20px #ffd700,0 0 40px #ffd700,0 0 60px #ff8800} }
        .predict-btn {
          background: #ffd700;
          color: #0a0a0f;
          border: none;
          padding: 16px 40px;
          font-family: 'Courier New', monospace;
          font-size: 16px;
          font-weight: bold;
          letter-spacing: 3px;
          cursor: pointer;
          text-transform: uppercase;
          transition: all 0.2s;
          clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
        }
        .predict-btn:hover { background: #fff; transform: scale(1.05); box-shadow: 0 0 30px #ffd700; }
        .predict-btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }
        .name-input {
          background: transparent;
          border: none;
          border-bottom: 2px solid #ffd700;
          color: #ffd700;
          font-family: 'Courier New', monospace;
          font-size: 20px;
          padding: 10px 4px;
          width: 100%;
          outline: none;
          text-align: center;
          letter-spacing: 2px;
          box-sizing: border-box;
        }
        .name-input::placeholder { color: rgba(255,215,0,0.3); }
        .reset-btn {
          background: transparent;
          border: 1px solid rgba(255,215,0,0.3);
          color: rgba(255,215,0,0.6);
          padding: 10px 24px;
          font-family: 'Courier New', monospace;
          font-size: 12px;
          letter-spacing: 2px;
          cursor: pointer;
          transition: all 0.2s;
          text-transform: uppercase;
        }
        .reset-btn:hover { border-color: #ffd700; color: #ffd700; }
      `}</style>

      <div style={{
        position: "relative", zIndex: 1,
        width: "100%", maxWidth: "620px",
        border: "1px solid rgba(255,215,0,0.2)",
        padding: "48px 40px",
        background: "rgba(10,10,15,0.95)",
        boxShadow: "0 0 80px rgba(255,215,0,0.05), inset 0 0 40px rgba(255,215,0,0.02)",
        boxSizing: "border-box",
      }}>
        <div style={{ position: "absolute", inset: 0, overflow: "hidden", pointerEvents: "none", zIndex: 10 }}>
          <div style={{
            position: "absolute", left: 0, right: 0, height: "2px",
            background: "linear-gradient(transparent, rgba(255,215,0,0.1), transparent)",
            animation: "scanline 4s linear infinite",
          }} />
        </div>

        <div style={{ textAlign: "center", marginBottom: "40px" }}>
          <div style={{ fontSize: "11px", letterSpacing: "6px", color: "rgba(255,215,0,0.4)", marginBottom: "12px" }}>
            ◈ CLASSIFIED ORACLE SYSTEM v3.1 ◈
          </div>
          <h1 style={{
            color: "#ffd700", fontSize: "36px", margin: 0,
            fontWeight: "bold", letterSpacing: "4px",
            animation: "glow 3s ease-in-out infinite",
          }}>
            DAY PROPHET
          </h1>
          <div style={{ color: "rgba(255,215,0,0.3)", fontSize: "11px", letterSpacing: "3px", marginTop: "8px" }}>
            ACCURACY RATE: 100%*
          </div>
          <div style={{ color: "rgba(255,215,0,0.15)", fontSize: "9px", marginTop: "4px" }}>
            *results may not be accurate
          </div>
        </div>

        {phase === "idle" && (
          <div style={{ animation: "slideUp 0.4s ease" }}>
            <div style={{ marginBottom: "32px" }}>
              <div style={{ color: "rgba(255,215,0,0.5)", fontSize: "11px", letterSpacing: "3px", marginBottom: "16px", textAlign: "center" }}>
                ENTER SUBJECT NAME
              </div>
              <input
                className="name-input"
                value={name}
                onChange={(e) => setName(e.target.value)}
                onKeyDown={(e) => e.key === "Enter" && runPrediction()}
                placeholder="who are you..."
                maxLength={30}
              />
            </div>
            <div style={{ textAlign: "center" }}>
              <button className="predict-btn" onClick={runPrediction} disabled={!name.trim()}>
                ⚡ Predict My Day
              </button>
            </div>
          </div>
        )}

        {phase === "loading" && (
          <div style={{ animation: "slideUp 0.3s ease" }}>
            <div style={{ color: "rgba(255,215,0,0.5)", fontSize: "11px", letterSpacing: "3px", textAlign: "center", marginBottom: "32px" }}>
              PROCESSING: {name.toUpperCase()}
            </div>
            <div style={{ display: "flex", flexDirection: "column", gap: "16px" }}>
              {steps.map((step, i) => {
                const done = i < currentStep;
                const active = i === currentStep;
                return (
                  <div key={i} style={{
                    display: "flex", alignItems: "center", gap: "16px",
                    padding: "14px 20px",
                    border: `1px solid ${active ? "rgba(255,215,0,0.6)" : done ? "rgba(255,215,0,0.2)" : "rgba(255,215,0,0.05)"}`,
                    background: active ? "rgba(255,215,0,0.05)" : "transparent",
                    transition: "all 0.4s",
                    opacity: i > currentStep ? 0.25 : 1,
                  }}>
                    <span style={{ fontSize: "20px" }}>{step.icon}</span>
                    <span style={{
                      flex: 1, color: done ? "rgba(255,215,0,0.5)" : active ? "#ffd700" : "rgba(255,215,0,0.3)",
                      fontSize: "13px", letterSpacing: "1px",
                      animation: active ? "flicker 0.8s infinite" : "none",
                    }}>
                      {step.text}
                    </span>
                    <span style={{ fontSize: "14px", color: done ? "#4cff91" : "#ffd700" }}>
                      {done ? "✓" : active ? "▮" : "○"}
                    </span>
                  </div>
                );
              })}
            </div>
            <div style={{ marginTop: "24px", textAlign: "center", color: "rgba(255,215,0,0.3)", fontSize: "10px", letterSpacing: "2px" }}>
              DO NOT CLOSE — QUANTUM ENTANGLEMENT IN PROGRESS
            </div>
          </div>
        )}

        {phase === "done" && (
          <div style={{ animation: "slideUp 0.5s ease" }}>
            <div style={{ textAlign: "center", marginBottom: "28px" }}>
              <div style={{ fontSize: "52px", marginBottom: "8px", animation: "pulse 2s infinite" }}>{mood}</div>
              <div style={{ color: "rgba(255,215,0,0.5)", fontSize: "11px", letterSpacing: "4px" }}>
                ORACLE VERDICT FOR {name.toUpperCase()}
              </div>
            </div>
            <div style={{
              border: "1px solid rgba(255,215,0,0.3)",
              padding: "28px",
              background: "rgba(255,215,0,0.03)",
              position: "relative",
              marginBottom: "28px",
            }}>
              <p style={{
                color: "#ffe88a", fontSize: "17px", lineHeight: "1.7",
                margin: 0, textAlign: "center", letterSpacing: "0.5px",
              }}>
                {prediction}
              </p>
            </div>
            <div style={{
              display: "flex", justifyContent: "space-between",
              padding: "10px 0", borderTop: "1px solid rgba(255,215,0,0.1)", marginBottom: "24px",
            }}>
              {["CONFIDENCE: 99.9%", "SOURCE: CLASSIFIED", "STATUS: DOOMED"].map((tag, i) => (
                <div key={i} style={{ color: "rgba(255,215,0,0.25)", fontSize: "9px", letterSpacing: "1px" }}>{tag}</div>
              ))}
            </div>
            <div style={{ textAlign: "center" }}>
              <button className="reset-btn" onClick={reset}>↩ Try Again (it won't help)</button>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
``.
