<div align="center">

# 🤖 PID-Controlled LEGO EV3 Robot

<br>

> **Can a robot drive in a perfectly straight line?**
> Not without feedback control — and that's exactly what we built.

<br>

[![Watch Demo](https://img.shields.io/badge/🎬_Watch_Demo-LinkedIn_Video-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/posts/ahtisham-salim_its-much-pleasure-to-share-my-control-system-activity-7166161920641769472-hgGq)

<br>

![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-E16737?style=flat-square&logo=mathworks&logoColor=white)
![LEGO EV3](https://img.shields.io/badge/LEGO-EV3%20Mindstorms-FDD835?style=flat-square&logo=lego&logoColor=black)
![PID](https://img.shields.io/badge/Controller-PID%20(Closed%20Loop)-purple?style=flat-square)
![Namal](https://img.shields.io/badge/Namal%20University-EE%20361L-teal?style=flat-square)

---

</div>

## The Problem

When you send the same power to both wheels of a differential-drive robot, it **doesn't go straight**. Mechanical differences, surface friction, and motor tolerances cause the robot to drift and skew. The more it runs, the worse it gets.

**Open-loop control can't fix this.** You need feedback.

## The Solution

We implemented a **closed-loop PID controller** on a LEGO Mindstorms EV3 robot using MATLAB/Simulink. The controller reads encoder values from both wheel motors, computes the rotation difference (error), and adjusts individual wheel speeds in real-time to keep the robot tracking a straight line.

The result? **Encoder output mismatch stays near zero** — the robot drives straight, every time.

## How It Works

```
                    ┌─────────────────────────┐
                    │     DESIRED PATH        │
                    │     (Straight Line)     │
                    └───────────┬─────────────┘
                                │
                                ▼
                    ┌───────────────────────┐
          ┌────────│     PID CONTROLLER     │────────┐
          │        │                       │        │
          │        │  Error = L_enc - R_enc │        │
          │        │  Correction = Kp × e   │        │
          │        └───────────────────────┘        │
          │                                          │
          ▼                                          ▼
   ┌──────────────┐                        ┌──────────────┐
   │ RIGHT MOTOR  │                        │  LEFT MOTOR  │
   │  (Port B)    │                        │  (Port C)    │
   │              │                        │              │
   │  Speed + Δ   │                        │  Speed - Δ   │
   └──────┬───────┘                        └──────┬───────┘
          │                                        │
          ▼                                        ▼
   ┌──────────────┐                        ┌──────────────┐
   │   ENCODER    │                        │   ENCODER    │
   │  (Rotation)  │                        │  (Rotation)  │
   └──────┬───────┘                        └──────┬───────┘
          │                                        │
          └──────────── FEEDBACK ──────────────────┘
                          │
                          ▼
                   Rotation Diff → Back to PID
```

**In plain English:**
- The PID controller watches both wheel encoders
- If the left wheel spins faster → it slows it down
- If the right wheel lags → it speeds it up
- The correction happens every cycle — the robot self-corrects in real-time

## Open Loop vs Closed Loop

| | Open Loop | Closed Loop (PID) |
|---|---|---|
| **Feedback** | None | Continuous encoder feedback |
| **Straight line?** | Drifts over time | Stays on track |
| **Error correction** | Manual only | Automatic, real-time |
| **Encoder mismatch** | Grows unbounded | Stays near zero |

## Tech Stack

| What | Details |
|------|---------|
| **Robot** | LEGO Mindstorms EV3 (differential drive) |
| **Controller** | PID (Proportional control for straight-line sync) |
| **Software** | MATLAB R2023a + Simulink |
| **Deployment** | Build, Deploy & Start → runs standalone on EV3 brick |
| **Motors** | Port B (Right Wheel) + Port C (Left Wheel) |
| **Sensors** | Built-in motor encoders (rotation feedback) |
| **Simulink Model** | `ev3_drive_closedloop` |

## Simulink Architecture

The Simulink model has two main subsystems:

**PID Controller Block** — Takes the rotation difference between left and right encoders, computes a proportional correction, and adjusts individual wheel speeds. During turns, synchronization is disabled.

**Motors Block** — Contains simulated motor models (for offline testing) and actual LEGO EV3 motor/encoder blocks (for hardware deployment). Right wheel on Port B, left wheel on Port C.

## Results

The closed-loop simulation confirmed that **encoder output mismatch stays near zero** throughout the run — meaning the robot maintains a straight trajectory. After deploying to the actual EV3 hardware via Simulink's "Build, Deploy & Start", the physical robot replicated the simulation behavior and drove in a straight line.

## 🎬 Demo Video

<div align="center">

[![LinkedIn Demo Video](https://img.shields.io/badge/▶_Watch_the_Robot_in_Action-LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/posts/ahtisham-salim_its-much-pleasure-to-share-my-control-system-activity-7166161920641769472-hgGq)

*Click above to see the LEGO EV3 robot driving straight using PID closed-loop control!*

</div>

## Repository Contents

```
PID-Controlled-Lego-EV3-Robot/
│
├── README.md                         # You're reading it
└── Control_Systems_Lab13_Report.pdf  # Full lab report with Simulink diagrams & results
```

> The PDF report includes all Simulink block diagrams (closed-loop model, PID controller internals, motor subsystem), encoder output scope plots, and simulation graphs.

## The Team

| | Name | Roll No. |
|---|------|---------|
| 🛠️ | **Ahtisham Saleem** | NIM-BSEE-2021-19 |
| 🛠️ | **Muhammad Yousaf** | NIM-BSEE-2021-31 |
| 🛠️ | **Allah Nawaz Khan** | NIM-BSEE-2021-40 |

## Academic Context

**Course:** EE 361L — Control Systems Lab · **Lab 13** (Final Lab)
**Instructor:** Dr. Sami ud Din · **Lab Engineer:** Engr. Faizan Ahmad
**University:** Namal University, Mianwali · **Semester:** Fall 2023

## What We Learned

This wasn't just a simulation exercise — we **built the robot from scratch**, assembled the LEGO components, designed the Simulink model, simulated it, deployed it to real hardware, and watched it drive. The gap between "it works in simulation" and "it works on the table" is where the real engineering happens.

---

<div align="center">

**Built with LEGO bricks, controlled with math.**

[![Email](https://img.shields.io/badge/Email-engr.ahtishamsaleem%40gmail.com-red?style=flat-square&logo=gmail)](mailto:engr.ahtishamsaleem@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Ahtisham%20Salim-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/ahtisham-salim)
[![GitHub](https://img.shields.io/badge/GitHub-codebyahtisham-181717?style=flat-square&logo=github)](https://github.com/codebyahtisham)

⭐ **Star this repo if you think PID controllers are cool!** ⭐

</div>
