```mermaid
flowchart TD
    subgraph "User Interaction Layer (User is God! :D)"
        UI["Frontend / SPA (React) - Real-Time Dashboard (Agent Progress, Achievements, What-If Scenarios, Iteration Controls)"]
    end

    subgraph "gangAi Core Server (The Brain!)"
        VS_IO["Vector Store (RAG/Memory) - Context, Learning, Simulation & Rollback Data"]
        LLM_ORCH["LLM Orchestrator (Local Model: Decision Maker, Queue Manager, Priority Queue, Rollback Engine, Iteration Handler)"]
        MCP["MCP Server (Universal Tool Executor - Non-Blocking, Interruptible, Resilient)"]
    end

    subgraph "Tools & Execution Layer"
        TOOLS["Tools / APIs (e.g., simulation_engine(), predictive_model(), what_if_analyzer())"]
    end

    subgraph "Premium Features (Cha-Ching!)"
        TTS["TTS Server (Amelia) - Premium Audio Streaming"]
    end

    subgraph "Agentic System (Scalable: 1000+ Agents with Hierarchy & User Iterations)"
        AGENTIC["Agentic Planner (Supervises, Plans Iterations, Streams What-If Results to UI)"]
        QUEUE["Task Queue (Smart Routing, Ultra-High Priority, Rollback & Iteration Support)"]
        subgraph "Mid-Level Coordinators"
            COORD_RESEARCH["Research Coordinator: Oversees Predictive Data & Scenarios"]
            COORD_DECIDE["Decision Coordinator: Oversees Strategy Optimization"]
            COORD_COMPILE["Compilation Coordinator: Oversees Scenario Integration"]
        end
        subgraph "Low-Level Executors"
            EXEC_RESEARCH["Executor Agents: Predictive Modeling, What-If Scenarios"]
            EXEC_DECIDE["Executor Agents: Strategy Optimization, Risk Prediction"]
            EXEC_COMPILE["Executor Agents: Final Predictions, Iteration Synthesis"]
        end
    end

    %% Expert Case Flow
    UI -->|"Ultra-Complex Query (e.g., Optimize global strategy with what-if scenarios?)"| gangAi_Core_Server
    VS_IO -->|"Context Output (RAG)"| LLM_ORCH
    LLM_ORCH -->|"Delegate Predictive Tasks + Iterations"| AGENTIC
    AGENTIC -->|"Plan & Spin What-If Layers"| QUEUE
    QUEUE -->|"Ultra-High Priority Routing"| COORD_RESEARCH
    QUEUE -->|"Ultra-High Priority Routing"| COORD_DECIDE
    QUEUE -->|"Ultra-High Priority Routing"| COORD_COMPILE
    COORD_RESEARCH -->|"Run Scenarios + Stream Progress to UI"| EXEC_RESEARCH
    COORD_DECIDE -->|"Optimize Strategies + Stream Updates to UI"| EXEC_DECIDE
    COORD_COMPILE -->|"Synthesize Iterations + Stream Milestones to UI"| EXEC_COMPILE
    EXEC_RESEARCH -->|"Execute + Report to UI (e.g., Modeled Scenarios)"| TOOLS
    EXEC_DECIDE -->|"Execute + Report to UI (e.g., Optimized Strategies)"| TOOLS
    EXEC_COMPILE -->|"Execute + Report to UI (e.g., Predicted Outcomes)"| TOOLS
    EXEC_RESEARCH -->|"Predictive Data"| COORD_RESEARCH
    COORD_RESEARCH -->|"Scenario Results"| COORD_DECIDE
    COORD_DECIDE -->|"Optimized Strategies"| COORD_COMPILE
    COORD_COMPILE -->|"Final Predictions + Iteration Report"| AGENTIC
    AGENTIC -->|"Iterated Strategy + Comprehensive UI Update"| LLM_ORCH
    LLM_ORCH -->|"Polished Response + UX Stream (e.g., 🤔 Optimizing Global Strategy)"| UI
    LLM_ORCH -.->|"Optional Premium"| TTS
    TTS -->|"Audio Stream"| UI
    UI -.->|"Feedback Loop (Iterate/Rollback)"| VS_IO
    LLM_ORCH -->|"Memory Update (Real-Time)"| VS_IO
    AGENTIC -.->|"Iteration & Prediction Logs"| VS_IO
    UI -->|"Interrupt/Step-In/Rollback/Iterate (God-Mode)"| AGENTIC
    UI -->|"Interrupt/Step-In/Rollback/Iterate (God-Mode)"| QUEUE
    UI -->|"Iterative Feedback (Refine Scenarios)"| LLM_ORCH

    %% Styling
    classDef investorStyle fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#000;
    classDef agentStyle fill:#f3e5f5,stroke:#4a148c,stroke-width:2px,color:#000;
    classDef premiumStyle fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#000;
    classDef midStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px,color:#000;
    classDef lowStyle fill:#fffde7,stroke:#f57f17,stroke-width:2px,color:#000;
    class UI,VS_IO,LLM_ORCH,MCP investorStyle;
    class AGENTIC,QUEUE agentStyle;
    class TTS premiumStyle;
    class TOOLS default;
    class COORD_RESEARCH,COORD_DECIDE,COORD_COMPILE midStyle;
    class EXEC_RESEARCH,EXEC_DECIDE,EXEC_COMPILE lowStyle;
