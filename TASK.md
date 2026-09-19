# Mechanical Engineering Automation Platform v2

Rebuild the Mechanical Engineering Automation Platform as a fully self-contained static HTML site with all calculations running client-side in JavaScript (no backend server needed).

## Requirements

### Design
- Modern, polished dark UI with smooth animations and transitions
- Professional engineering aesthetic — clean, precise, technical
- Responsive layout (desktop + mobile)
- Sidebar navigation with categorized tools
- Results displayed in attractive cards with color-coded pass/fail indicators
- Subtle grid background, glassmorphism touches, accent glow effects

### Tools (8 calculation modules)
1. **Cable Sizing** — IEC 60364-5-52 / BS 7671 (power, voltage, PF, length, cable type, installation method, max VD%, ambient temp)
2. **Transformer Sizing** — diversified load + growth margin (load kW, PF, diversity, margin, voltage ratio)
3. **Short Circuit Analysis** — fault current at transformer bus (kVA, voltage, impedance%, feeder impedance)
4. **Cooling Load Estimate** — simplified heat gain (area, ceiling height, occupants, equipment, lighting, windows, U-value, temps)
5. **Pipe Sizing** — Darcy-Weisbach friction loss (flow rate, length, pressure drop, fluid type, fittings)
6. **Pump Sizing** — hydraulic power + motor selection (flow rate, total head, density, efficiency)
7. **Beam Deflection Check** — simply supported, midspan (span, load, load type, E, section properties)
8. **Column Buckling Check** — Euler/Johnson (length, load, section, end conditions, yield strength)

### Additional Features
- **Single Line Diagram (SLD) Builder** — drag-and-drop canvas with generator, transformer, breaker, bus, motor, load components. Export to SVG/PNG.
- **Engineering Report Generator** — generates a professional multi-section report (cover, executive summary, scope, input data, methodology, results, discussion, conclusion, assumptions, references, signature block) from calculation results. Export to PDF or print.

### Technical
- Single `index.html` file with embedded CSS and JS
- All calculation logic in JavaScript (ported from the Python backend)
- No external dependencies except Google Fonts (Inter, JetBrains Mono)
- All state in-memory (no localStorage needed but okay to use)
- API status indicator shows "Ready" immediately (no backend call)

### Calculation Accuracy
Port the existing Python calculation logic faithfully:
- Cable: load current, derating (installation + ambient), standard cable sizes, voltage drop (sqrt(3)*I*R*L), pass/fail
- Transformer: S = kW/PF, diversified = S/diversity, kva = diversified*(1+margin), standard sizes
- Short circuit: Z_base = V²/S, Z_total = Z%*Z_base + Z_feeder, Ik = V/(sqrt(3)*Z), momentary = Ik*1.15
- Cooling load: envelope = area*U*ΔT, occupants (75W sensible + 60W latent each), equipment, lighting*1.2, total/3.517 = tons
- Pipe: iterative diameter search, Darcy-Weisbach, Reynolds, Colebrook-White, fittings K-factors
- Pump: P_hyd = ρ*g*Q*H, P_shaft = P_hyd/η, motor = next standard size with 1.1 service factor
- Beam: deflection formulas for point/UDL/fixed, L/250 limit, stress = M*y/I
- Column: slenderness ratio, Euler (λ>100) vs Johnson (λ≤100), FoS ≥ 1.5

### Output
Write the complete site to: `/c/Users/USER/mechanical-automation-site-v2/index.html`

Make it production-quality. This is a real engineering tool that will be published live.
