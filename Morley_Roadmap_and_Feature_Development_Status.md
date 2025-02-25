## Morley Roadmap and Feature Development Status

### Overview  
This roadmap outlines the planned development stages for Morley, detailing the current status, upcoming features, and long-term vision. It provides transparency to the community and encourages contributions by clearly stating priorities and development phases.

---

### Current Status

Morley is under active development, focusing on creating an integrated ecosystem for compiling Ladder Logic and Structured Text into Plutus smart contracts on Cardano. Here’s what’s currently working:

1. **ArkWriter (Web-Based IDE)**  
   - Basic UI for creating and editing Ladder Logic diagrams.  
   - Complete library of mappings for Ladder Logic (.ll) and Structured Text (.st).  
   - Saving and exporting `.ll` files for Ladder Logic and `.st` files for Structured Text.  
   - Integrated CIP-30 wallet connector (ready for future interactions).  

2. **Morley-Core (Compiler Engine)**  
   - **Ladder Logic to IR:** Intermediate Representation (IR) parser for converting Ladder Logic into structured IR format.  
   - **Structured Text to IR:** Complete mappings for converting Structured Text into IR, ensuring compatibility with OpenPLC constructs.  
   - **Reverse Compiler:** Initial development for reversing compiled Plutus scripts back into machine-readable Ladder Logic and Structured Text.  
   - **PlutusLadder Compiler (PLC):** Early-stage development for compiling both Ladder Logic and Structured Text into Plutus Core.  
   - **Hybrid 2-Layer Time Logic:** Specification is complete with an anchoring mechanism and verifiable hash format.  

3. **Educational Resources and Documentation**  
   - Comprehensive guides for new developers, including Ladder Logic basics, Structured Text, and the Morley vision.  
   - Introduction to Plutus and Cardano smart contracts.  
   - Setup instructions and environment configuration guides.  

---

### Short-Term Milestones (Q1 2025)

1. **ArkWriter Improvements**  
   - Enhanced UI/UX for a more intuitive design experience for both Ladder Logic and Structured Text.  
   - Real-time validation of Ladder Logic and Structured Text syntax.  
   - Drag-and-drop functionality for Ladder Logic elements.  
   - Auto-completion and syntax checking for Structured Text.  

2. **Morley-Core Enhancements**  
   - **IR-to-Plutus Compilation Pipeline:** Complete the pipeline for compiling Ladder Logic and Structured Text into Plutus Core.  
   - **PlutusLadder Compiler (PLC):** Basic functionality for simple Ladder Logic and Structured Text scenarios.  
   - **Reverse Compilation:** Initial implementation to retrieve on-chain state changes back as machine-readable Ladder Logic and Structured Text.  
   - Full feature parity with OpenPLC for fundamental Ladder Logic and Structured Text constructs.  

3. **Hybrid 2-Layer Time Logic Implementation**  
   - Develop dual-layer time logic for real-time execution on Layer 2 (Hydra/Midgard) and slot-based validation on Layer 1 (Cardano).  
   - Implement anchoring mechanism and verifiable hash format for time validation.  
   - Ensure compatibility with reverse compiler to preserve time logic in Ladder Logic and Structured Text.  

4. **Structured Text Support Expansion - *COMPLETE**  
   - Comprehensive support for Structured Text programming, including:  
     - Basic instructions (IF-THEN-ELSE, CASE, FOR, WHILE)  
     - Advanced operations (Arithmetic, Bitwise, String Manipulation)  
     - Function calls and modular programming  
   - Bidirectional compilation support, allowing Structured Text to be compiled to Plutus and then retrieved back as machine-readable Structured Text.  

5. **Educational Content Expansion**  
   - More example programs and `.ll`/`.st` files for users to experiment with.  
   - Detailed “Getting Started” guides with practical examples for both Ladder Logic and Structured Text.  
   - Interactive tutorials to help users understand the Morley workflow.  

6. **Community Engagement and Feedback Loop**  
   - Public release and open-sourcing of all active repositories.  
   - Gathering community feedback through GitHub issues and discussions.  
   - Actively involving early adopters and contributors in testing and feature requests.  

---

### Mid-Term Milestones (Q2 – Q3 2025)

1. **Full Functionality for PlutusLadder Compiler (PLC)**  
   - Complete support for compiling Ladder Logic and Structured Text to Plutus Core.  
   - Support for complex constructs, including:  
     - **Ladder Logic:** Nested conditions, advanced timers, counters, and bitwise operations.  
     - **Structured Text:** Complex expressions, nested loops, and custom functions.  
   - Optimization for efficient Plutus script generation and gas cost reduction.  

2. **Bidirectional Flow and Reverse Compilation**  
   - Implementing reverse compilation to retrieve on-chain state changes as machine-readable Ladder Logic and Structured Text.  
   - Ensuring full feature parity with OpenPLC for bidirectional flow.  
   - Visualization tools in ArkWriter to display state changes as Ladder Logic diagrams or Structured Text code.  

3. **ArkHunter & ArkTracer**  
   - **ArkHunter:** Cardano network parameter simulation and analysis tool.  
     - Simulates and evaluates protocol parameter changes.  
     - Visualizes cause-and-effect relationships between parameter shifts.  
     - Predictive simulations and historical analysis for governance decision-making.  
   - **ArkTracer:** Plutus script debugger and execution flow visualizer.  
     - Real-time debugging and step-through execution.  
     - Displays transaction validation status and error messages.  
     - Visualizes execution flow for enhanced debugging.  

4. **PlutusLadderSim (PLS) – Simulator Integration**  
   - Simulation environment for testing both Ladder Logic and Structured Text smart contracts before on-chain deployment.  
   - Real-time monitoring of state changes and contract interactions.  
   - Integration with ArkWriter for seamless simulation and visualization.  

5. **Comprehensive Testing and Security Audits**  
   - Extensive testing for compilation accuracy and contract execution.  
   - Security audits to ensure smart contracts are secure and resistant to vulnerabilities.  
   - Community-driven testing and bug bounties to enhance reliability.  

---

### Long-Term Vision (Q4 2025 and Beyond)

1. **Full Feature Parity with OpenPLC**  
   - Complete support for all Ladder Logic and Structured Text constructs and advanced programming elements.  
   - Full compatibility with OpenPLC’s instruction set, ensuring a seamless transition for industrial engineers.  

2. **Morley-Plutus Dual-Script Architecture**  
   - Dual-script architecture for hybrid execution on Cardano L1 and Layer 2 sidechains (Hydra, Midgard).  
   - Ensures trustless state synchronization between on-chain and off-chain environments.  
   - Enables real-time automation on sidechains with state validation on L1.  

3. **Integration with Industrial IoT and Edge Devices**  
   - Enabling interaction with industrial IoT devices for decentralized automation.  
   - Support for edge computing to reduce latency and enhance real-time control.  
   - Integration with existing industrial communication protocols (e.g., Modbus, OPC-UA).  

---

### Community Involvement

Morley is open-source, and community contributions are encouraged. Here’s how you can get involved:  
- **Feature Requests and Feedback:** Use GitHub issues to suggest features or report bugs.  
- **Code Contributions:** Submit pull requests to help with ongoing development.  
- **Testing and Bug Reports:** Test the current functionality and report issues.  
- **Documentation Help:** Improve documentation to make it easier for new users.  

---

### Moving Forward

- **Public Release:** Announce and open-source all active repositories.  
- **Gather Feedback:** Actively engage with early adopters and contributors.  
- **Prioritize Development:** Use community feedback to prioritize features.  
- **Continue Development:** Focus on completing the PlutusLadder Compiler, Reverse Compiler, and bidirectional flow.  

