```mermaid
flowchart TD
    subgraph "User Interaction Layer (User is God! :D)"
        UI["Frontend / SPA (React) - Real-Time Dashboard (Agent Progress, Achievements)"]
    end

    subgraph "gangAi Core Server (The Brain!)"
        VS_IO["Vector Store (RAG/Memory) - Context & Learning"]
        LLM_ORCH["LLM Orchestrator (Local Model: Decision Maker, Queue Manager, Priority Queue)"]
        MCP["MCP Server (Universal Tool Executor - Non-Blocking)"]
    end

    subgraph "Tools & Execution Layer"
        TOOLS["Tools / APIs (e.g., business_search(), risk_assess())"]
    end

    subgraph "Premium Features (Cha-Ching!)"
        TTS["TTS Server (Amelia) - Premium Audio Streaming"]
    end

    subgraph "Agentic System (Scalable: 1000+ Agents with Hierarchy)"
        AGENTIC["Agentic Planner (Supervises, Plans, Reports to UI)"]
        QUEUE["Task Queue (Smart Routing, Priority Handling)"]
        subgraph "Mid-Level Coordinators"
            COORD_RESEARCH["Research Coordinator: Oversees Data Gathering"]
            COORD_DECIDE["Decision Coordinator: Oversees Evaluation"]
            COORD_COMPILE["Compilation Coordinator: Oversees Aggregation"]
        end
        subgraph "Low-Level Executors"
            EXEC_RESEARCH["Executor Agents: Market Analysis, Data Scraping"]
            EXEC_DECIDE["Executor Agents: Needs Evaluation, Offer Customization"]
            EXEC_COMPILE["Executor Agents: Insights Aggregation"]
        end
    end

    %% Medium Case Flow
    UI -->|"Deep Query (e.g., Businesses struggling in Vilnius? Offer loans/stake)"| gangAi_Core_Server
    VS_IO -->|"Context Output (RAG)"| LLM_ORCH
    LLM_ORCH -->|"Delegate Deep Dive"| AGENTIC
    AGENTIC -->|"Plan & Delegate Tasks"| QUEUE
    QUEUE -->|"Route to Coordinators"| COORD_RESEARCH
    QUEUE -->|"Route to Coordinators"| COORD_DECIDE
    QUEUE -->|"Route to Coordinators"| COORD_COMPILE
    COORD_RESEARCH -->|"Coordinate + Stream Progress"| EXEC_RESEARCH
    COORD_DECIDE -->|"Coordinate + Stream Achievements"| EXEC_DECIDE
    COORD_COMPILE -->|"Coordinate + Stream Milestones"| EXEC_COMPILE
    EXEC_RESEARCH -->|"Execute + Report to UI (e.g., Gathered Profiles)"| TOOLS
    EXEC_DECIDE -->|"Execute + Report to UI (e.g., Assessed Risks)"| TOOLS
    EXEC_COMPILE -->|"Execute + Report to UI (e.g., Compiled Insights)"| TOOLS
    EXEC_RESEARCH -->|"Raw Data"| COORD_RESEARCH
    COORD_RESEARCH -->|"Aggregated Research"| COORD_DECIDE
    COORD_DECIDE -->|"Custom Decisions (e.g., Loan Terms)"| COORD_COMPILE
    COORD_COMPILE -->|"Final Report"| AGENTIC
    AGENTIC -->|"Compiled Decision + UI Update"| LLM_ORCH
    LLM_ORCH -->|"Polished Response + UX Stream (e.g., 🤔 Analyzing Vilnius Businesses)"| UI
    LLM_ORCH -.->|"Optional Premium"| TTS
    TTS -->|"Audio Stream"| UI
    UI -.->|"Feedback Loop"| VS_IO
    LLM_ORCH -->|"Memory Update"| VS_IO
    AGENTIC -.->|"Deep Dive Logs"| VS_IO
    UI -->|"Interrupt/Step-In/Rollback (God-Mode)"| AGENTIC

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
