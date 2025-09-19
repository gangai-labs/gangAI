```mermaid
flowchart TD
    subgraph "User Interaction Layer"
        UI["Frontend / SPA (React) - Any modern UX connecting to gangAi Server (Real-Time Updates: Agent Progress, Achievements, Interrupt Controls)"]
    end

    subgraph "gangAi Core Server"
        VS_IO["Vector Store (RAG/Memory) - Input/Output for Context & Learning (Updated in Real-Time)"]
        LLM_ORCH["LLM Orchestrator (Local Model: Decision Maker, Queue Manager, Priority Queue, Handles Interrupts & Rollbacks)"]
        MCP["MCP Server (Universal Tool Executor - Non-Blocking, Interruptible)"]
    end

    subgraph "Tools & Execution Layer"
        TOOLS["Tools / APIs / Generators (e.g., get_current_time(), error_debug(), business_search())"]
    end

    subgraph "Premium Features"
        TTS["TTS Server (Amelia) - Optional Premium Audio Streaming"]
    end

    subgraph "Agentic System (Scalable: Up to 1000+ Agents with Hierarchy & User Oversight)"
        AGENTIC["Agentic Planner (Top-Level: Supervises Hierarchy, Dynamically Spins Agents, Decision Planning, Deep Dive Mode, Real-Time Reporting to UI)"]
        QUEUE["Task Queue (Smart Routing, Unlimited Parallelism, Priority Handling, Interrupt & Rollback Support)"]
        subgraph "Mid-Level Coordinators (Hierarchical Layer: Coordinate Sub-Tasks, Report Progress/Achievements) "
            COORD_RESEARCH["Research Coordinator: Oversees Data Gathering, Streams Updates (e.g., 'Gathered X Profiles')"]
            COORD_DECIDE["Decision Coordinator: Oversees Evaluation, Streams Achievements (e.g., 'Assessed Y Risks')"]
            COORD_COMPILE["Compilation Coordinator: Oversees Aggregation, Streams Milestones (e.g., 'Compiled Z Insights')"]
        end
        subgraph "Low-Level Executors (Hierarchical Layer: Parallel Workers, User-Interruptible)"
            EXEC_RESEARCH["Executor Agents: Market Analysis, Data Scraping, etc. (Report Steps: 'Doing A', 'Achieved B')"]
            EXEC_DECIDE["Executor Agents: Needs Evaluation, Offer Customization (e.g., Loans/Stake) (Report: 'Evaluating C', 'Achieved D')"]
            EXEC_COMPILE["Executor Agents: Insights Aggregation, Risk Assessment (Report: 'Aggregating E', 'Achieved F')"]
        end
        AGENTS["All Agents (Non-Blocking, Parallel Execution Across Hierarchy, Real-Time UI Updates, User God-Mode: Interrupt All, Step-In, Windback/Rollback)"]
    end

    %% Main Flow (Easy Cases: e.g., Time Query or Error Debug)
    UI -->|"User Query (e.g., What is the time?)"| gangAi_Core_Server
    VS_IO -->|"Context Output (RAG)"| LLM_ORCH
    LLM_ORCH -->|"Easy Case: Simple Tool Decision"| MCP
    MCP -->|Execute| TOOLS
    TOOLS -->|Results| MCP
    MCP -->|"Stream Results"| LLM_ORCH
    LLM_ORCH -->|"Polish Response + Stream UX (e.g., 🤔 Calling get_current_time())"| UI
    LLM_ORCH -.->|"Optional Premium"| TTS
    TTS -->|"Audio Stream"| UI
    UI -.->|"Feedback Loop (User God-Mode: Interrupt/Step-In)"| VS_IO
    LLM_ORCH -->|"All Cases: Memory Update (Real-Time)"| VS_IO

    %% Medium/Complex Case Branch (Deep Dive with Hierarchy: e.g., Vilnius Business Analysis)
    LLM_ORCH -->|"Medium Case: Deep Query (e.g., Businesses struggling in Vilnius? Offer loans/stake, assess needs)"| AGENTIC
    AGENTIC -->|"Top-Level Planning: Delegate to Coordinators"| QUEUE
    QUEUE -->|"Prioritize & Route Down Hierarchy"| COORD_RESEARCH
    QUEUE -->|"Prioritize & Route Down Hierarchy"| COORD_DECIDE
    QUEUE -->|"Prioritize & Route Down Hierarchy"| COORD_COMPILE
    COORD_RESEARCH -->|"Coordinate Sub-Tasks + Stream Progress to UI"| EXEC_RESEARCH
    COORD_DECIDE -->|"Coordinate Sub-Tasks + Stream Achievements to UI"| EXEC_DECIDE
    COORD_COMPILE -->|"Coordinate Sub-Tasks + Stream Milestones to UI"| EXEC_COMPILE
    EXEC_RESEARCH -->|"Parallel Execution + Report Steps/Achievements to UI"| TOOLS
    EXEC_DECIDE -->|"Parallel Execution + Report Steps/Achievements to UI"| TOOLS
    EXEC_COMPILE -->|"Parallel Execution + Report Steps/Achievements to UI"| TOOLS
    EXEC_RESEARCH -->|"Raw Data (e.g., Market Trends, Profiles)"| COORD_RESEARCH
    COORD_RESEARCH -->|"Aggregated Research"| COORD_DECIDE
    COORD_DECIDE -->|"Custom Decisions (e.g., Loan Terms, Risks)"| COORD_COMPILE
    COORD_COMPILE -->|"Final Report"| AGENTIC
    AGENTIC -->|"Compiled Hierarchical Decision + Full UI Update"| LLM_ORCH
    AGENTIC -.->|"Deep Dive Logs & Learnings (Real-Time Update)"| VS_IO

    %% Hard Case Branch (Ultra-Complex: e.g., Multi-Region Business Strategy with Simulations)
    LLM_ORCH -->|"Hard Case: Ultra-Complex Query (e.g., Simulate global business impacts, optimize offers across regions, predict outcomes? Deep Dive + Simulations)"| AGENTIC
    AGENTIC -->|"Advanced Planning: Spin Extra Layers, Run Simulations"| QUEUE
    QUEUE -->|"High-Priority Routing + Simulation Tasks"| COORD_RESEARCH
    QUEUE -->|"High-Priority Routing + Simulation Tasks"| COORD_DECIDE
    QUEUE -->|"High-Priority Routing + Simulation Tasks"| COORD_COMPILE
    COORD_RESEARCH -->|"Simulate Data Scenarios + Stream Progress"| EXEC_RESEARCH
    EXEC_RESEARCH -->|"Simulated Results + Report Achievements"| COORD_RESEARCH
    COORD_DECIDE -->|"Optimize Offers via Models + Stream Updates"| EXEC_DECIDE
    EXEC_DECIDE -->|"Predicted Outcomes + Report Milestones"| COORD_DECIDE
    COORD_COMPILE -->|"Integrate Simulations + Final Predictions"| EXEC_COMPILE
    EXEC_COMPILE -->|"Aggregated Scenarios + UI Reports"| COORD_COMPILE
    AGENTIC -->|"Final Optimized Strategy + Comprehensive UI Summary"| LLM_ORCH

    %% User God-Mode Interventions (Global: Can Interrupt All Levels)
    UI -->|"User Interrupt: Step-In, Windback/Rollback, Override (God-Mode)"| LLM_ORCH
    UI -->|"User Interrupt: Step-In, Windback/Rollback, Override (God-Mode)"| AGENTIC
    UI -->|"User Interrupt: Step-In, Windback/Rollback, Override (God-Mode)"| QUEUE
    UI -->|"User Interrupt: Step-In, Windback/Rollback, Override (God-Mode)"| AGENTS
    AGENTIC -->|"Stream Agent Status/Achievements to UI (What Doing, What Achieved)"| UI
    COORD_RESEARCH -->|"Stream Coordinator Updates to UI"| UI
    COORD_DECIDE -->|"Stream Coordinator Updates to UI"| UI
    COORD_COMPILE -->|"Stream Coordinator Updates to UI"| UI
    EXEC_RESEARCH -->|"Stream Executor Steps/Achievements to UI"| UI
    EXEC_DECIDE -->|"Stream Executor Steps/Achievements to UI"| UI
    EXEC_COMPILE -->|"Stream Executor Steps/Achievements to UI"| UI

    %% Styling for Investor Appeal
    classDef investorStyle fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#000;
    classDef agentStyle fill:#f3e5f5,stroke:#4a148c,stroke-width:2px,color:#000;
    classDef premiumStyle fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#000;
    classDef midStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px,color:#000;
    classDef lowStyle fill:#fffde7,stroke:#f57f17,stroke-width:2px,color:#000;
    classDef hardStyle fill:#ffebee,stroke:#c62828,stroke-width:2px,color:#000;

    class UI,VS_IO,LLM_ORCH,MCP investorStyle;
    class AGENTIC,QUEUE,AGENTS agentStyle;
    class TTS premiumStyle;
    class TOOLS default;
    class COORD_RESEARCH,COORD_DECIDE,COORD_COMPILE midStyle;
    class EXEC_RESEARCH,EXEC_DECIDE,EXEC_COMPILE lowStyle;
