# AI Agent Incident Incidence Simulator

A small, browser-based experiment for making **rough estimates** of high-impact AI agent incidents. It started as a back-of-the-envelope calculation in a YouTube discussion, not as a research project.

The idea is simple: take a hypothetical number of publicly known incidents, assume some incidents never become public, account for a possible detection delay, and compare the resulting estimate with an assumed population of active agents.

## Try it

Open `ai_agent_incidence_simulator_fixed.html` in a browser. No installation, server, or dependencies required.

Adjust the sliders to explore different assumptions. The simulator displays:

- **Hidden-adjusted incidents:** known incidents multiplied by an assumed underreporting factor.
- **Growth-adjusted incidents:** the same estimate adjusted for growth during a hypothetical detection delay.
- **Incidents per agent:** adjusted incidents divided by the assumed active agent population, displayed as a percentage.
- **Risk ratio:** the same quotient expressed as approximately one incident per *X* agents.

The last two outputs are **scenario ratios**, not measured probabilities that an individual agent will cause an incident. They are not annual rates unless the input incidents and population are defined over a consistent one-year period.

## Original thought experiment

The initial example used these deliberately rough assumptions:

| Variable | Meaning | Example |
| --- | --- | ---: |
| `I_known` | Publicly known high-impact agent incidents | 20 |
| `M_hidden` | Multiplier for incidents not publicly known | 5× |
| `T_lag` | Assumed detection delay | 60 days |
| `g` | Assumed daily growth rate | 0.5% |
| `N_agents` | Assumed number of active agents | 10,000,000 |

The simplified calculation is:

```text
I_hidden_adjusted = I_known × M_hidden
I_growth_adjusted = I_hidden_adjusted × (1 + g)^T_lag
Scenario incidence (%) = I_growth_adjusted / N_agents × 100
Agents per estimated incident = N_agents / I_growth_adjusted
```

With the example settings:

```text
20 × 5 × (1.005)^60 ≈ 135 estimated incidents
135 / 10,000,000 × 100 ≈ 0.00135%
≈ 1 incident per 74,000 agents
```

These are **outputs of the assumptions**, not evidence that 135 such incidents actually occurred.

## What counts as an incident?

The discussion distinguished between:

- **Agent incidents:** an agent causes a consequential outcome during a sequence of actions, such as an unauthorized legal filing, a false police report, or an unintended purchase.
- **Action incidents:** an individual click, API call, form submission, or other action fails.
- **Low-impact failures:** formatting errors, broken links, spam, or incorrect API calls.
- **High-impact failures:** serious legal, security, financial, or other real-world consequences.

This simulator is concerned with the *high-impact agent-incident* category. It does **not** estimate failure rates per action.

## Limitations

This is a **toy model / thought experiment**, not a scientific study or a reliable prediction.

- The starting count of 20 was a casual guess, not the result of a systematic incident review.
- The agent population, hidden multiplier, detection delay, and growth rate are hypothetical inputs, not verified measurements.
- Applying a growth correction to incident counts assumes incidents scale with the chosen growth rate; that relationship is not established.
- Detection delays, reporting rates, and incident definitions may vary substantially.
- The model does not account for repeat incidents by the same agent, exposure time, agent activity levels, or uncertainty intervals.
- A ratio of incidents to agents should not be interpreted as the probability that a particular agent fails.

Use it to explore how assumptions affect a rough estimate—not to draw conclusions about real-world AI safety.

## Background

The original discussion also considered daily action volumes (e.g. 1,000 actions per narrow-definition agent or 20,000 per broad-definition agent). Those figures are **not used** in the simulator's current calculations.

And if you read this far: you've earned the *medal of reading weird posts on YouTube*.

## License

No license is specified here. Add a `LICENSE` file if you want to define reuse permissions.
