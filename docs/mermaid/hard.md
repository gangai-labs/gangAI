```mermaid
flowchart TD
    subgraph "User Interaction Layer (User is God! :D)"
        UI["Frontend / SPA (React) - Real-Time Dashboard (Agent Progress, Achievements, Simulation Results)"]
    end

    subgraph "gangAi Core Server (The Brain!)"
        VS_IO["Vector Store (RAG/Memory) - Context, Learning, Simulation Data"]
        LLM_ORCH["LLM Orchestrator (Local Model: Decision Maker, Queue Manager, Priority Queue, Rollback Engine)"]
        MCP["MCP Server (Universal Tool Executor - Non-Blocking, Interruptible)"]
    end

    subgraph "Tools & Execution Layer"
        TOOLS["Tools / APIs (e.g., business_search(), simulation_engine())"]
    end

    subgraph "Premium Features (Cha-Ching!)"
        TTS["TTS Server (Amelia) - Premium Audio Streaming"]
    end

    subgraph "Agentic System (Scalable: 1000+ Agents with Hierarchy)"
        AGENTIC["Agentic Planner (Supervises, Plans Simulations, Reports to UI)"]
        QUEUE["Task Queue (Smart Routing, High-Priority Simulation Tasks)"]
        subgraph "Mid-Level Coordinators"
            COORD_RESEARCH["Research Coordinator: Oversees Data & Simulation Scenarios"]
            COORD_DECIDE["Decision Coordinator: Oversees Offer Optimization"]
            COORD_COMPILE["Compilation Coordinator: Oversees Prediction Aggregation"]
        end
        subgraph "Low-Level Executors"
            EXEC_RESEARCH["Executor Agents: Market Analysis, Scenario Simulation"]
            EXEC_DECIDE["Executor Agents: Offer Optimization, Risk Modeling"]
            EXEC_COMPILE["Executor Agents: Aggregate Predictions, Final Reports"]
        end
    end

    %% Hard Case Flow
    UI -->|"Complex Query (e.g., Simulate global business impacts, optimize offers?)"| gangAi_Core_Server
    VS_IO -->|"Context Output (RAG)"| LLM_ORCH
    LLM_ORCH -->|"Delegate Simulation Tasks"| AGENTIC
    AGENTIC -->|"Plan & Spin Simulation Layers"| QUEUE
    QUEUE -->|"High-Priority Routing"| COORD_RESEARCH
    QUEUE -->|"High-Priority Routing"| COORD_DECIDE
    QUEUE -->|"High-Priority Routing"| COORD_COMPILE
    COORD_RESEARCH -->|"Simulate Scenarios + Stream Progress"| EXEC_RESEARCH
    COORD_DECIDE -->|"Optimize Offers + Stream Updates"| EXEC_DECIDE
    COORD_COMPILE -->|"Aggregate Predictions + Stream Milestones"| EXEC_COMPILE
    EXEC_RESEARCH -->|"Execute + Report to UI (e.g., Simulated Trends)"| TOOLS
    EXEC_DECIDE -->|"Execute + Report to UI (e.g., Optimized Offers)"| TOOLS
    EXEC_COMPILE -->|"Execute + Report to UI (e.g., Predicted Outcomes)"| TOOLS
    EXEC_RESEARCH -->|"Scenario Data"| COORD_RESEARCH
    COORD_RESEARCH -->|"Simulated Results"| COORD_DECIDE
    COORD_DECIDE -->|"Optimized Offers"| COORD_COMPILE
    COORD_COMPILE -->|"Final Predictions"| AGENTIC
    AGENTIC -->|"Compiled Strategy + UI Update"| LLM_ORCH
    LLM_ORCH -->|"Polished Response + UX Stream (e.g., 🤔 Simulating Global Impacts)"| UI
    LLM_ORCH -.->|"Optional Premium"| TTS
    TTS -->|"Audio Stream"| UI
    UI -.->|"Feedback Loop"| VS_IO
    LLM_ORCH -->|"Memory Update"| VS_IO
    AGENTIC -.->|"Simulation Logs"| VS_IO
    UI -->|"Interrupt/Step-In/Rollback (God-Mode)"| AGENTIC
    UI -->|"Interrupt/Step-In/Rollback (God-Mode)"| QUEUE

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
