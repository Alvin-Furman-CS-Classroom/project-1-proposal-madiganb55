# Automated Threat Response Recommendation System

## System Overview

The Automated Threat Response Recommendation System is an AI-powered cybersecurity solution that monitors network traffic for potential intrusions and generates optimized response recommendations. The system processes real-time log entries using Propositional Logic to detect potential attacks, classifies their severity using Machine Learning, and assesses system vulnerabilities to provide actionable response plans.

The system operates through five interconnected modules. Module 1 uses Propositional Logic rules to detect threats from network log entries, identifying suspicious patterns like port scans or brute force attempts. Module 2 applies Machine Learning classification to assign severity levels to detected threats, enabling prioritization. Module 3 assesses the current system state, identifying vulnerable components and their risk levels by combining threat data with live system health metrics.

Module 4 generates candidate response actions using Propositional Logic rules that match threat types and system states to appropriate mitigation strategies. Finally, Module 5 employs A* search to explore action sequences, optimizing for both speed of attack mitigation and minimal system disruption cost. The search algorithm uses the candidate responses as constraints, finding optimal paths through the action space.

This theme naturally integrates multiple AI techniques: Propositional Logic for rule-based detection and recommendation, Machine Learning for threat classification, and Search for response optimization. The intrusion response domain requires both knowledge-based reasoning (matching threats to responses) and optimization (finding the best action sequence), making it an ideal application for exploring these core AI concepts.

## Modules

### Module 1: Threat Detection

**Topics:** Propositional Logic

**Input:** Real-time network traffic log entries in structured format (e.g., JSON or syslog format) containing fields such as timestamp, source IP address, destination IP address, port numbers, connection status, and packet flags. Example: `{"timestamp": "2024-01-15T14:23:45Z", "src_ip": "192.168.1.100", "dst_ip": "10.0.0.5", "port": 22, "status": "failed"}`

**Output:** A threat detection report (JSON format) containing detected potential attacks with attributes: threat ID, threat type (e.g., "suspicious_port_scan", "brute_force_attempt"), source IP, target system, timestamp, and confidence level. Example: `{"threat_id": "T001", "type": "suspicious_port_scan", "src_ip": "192.168.1.100", "target": "10.0.0.5", "timestamp": "2024-01-15T14:23:45Z", "confidence": 0.85}`

**Integration:** This module's threat detection report feeds into Module 2 (Threat Severity Classification) for severity analysis and Module 3 (System State Assessment) for identifying vulnerable systems. The detected threats provide the foundation for all subsequent response recommendations.

**Prerequisites:** Course content on Propositional Logic (entailment, knowledge bases, inference methods, chaining, CNF, resolution). No prior modules required as this is the system entry point.

---

### Module 2: Threat Severity Classification

**Topics:** Machine Learning

**Input:** The threat detection report from Module 1 (JSON format) containing detected threats with their attributes. The module processes this report to extract features for classification.

**Output:** A threat severity report (JSON format) containing each threat ID mapped to a severity level (e.g., "critical", "high", "medium", "low") and a numerical severity score (0.0-1.0). Example: `{"threat_id": "T001", "severity_level": "high", "severity_score": 0.75, "rationale": "targeted_multiple_ports"}`

**Integration:** The severity classification output is used by Module 4 (Rule-Based Response Recommendation) to prioritize responses and by Module 5 (Search-Based Response Recommendation) to weight the importance of addressing different threats in the optimization process.

**Prerequisites:** Course content on Machine Learning (classification algorithms, feature extraction). Requires Module 1's threat detection report as input. 

---

### Module 3: System State Assessment

**Topics:** Data Processing

**Input:** The threat detection report from Module 1 (JSON format) and live system health metrics (JSON format) containing real-time data such as server load, active connections, system vulnerabilities, patch status, and resource utilization. Example system health: `{"servers": [{"id": "S001", "load": 0.85, "vulnerabilities": ["CVE-2023-1234"], "patched": false}], "network_status": "normal"}`

**Output:** A system state assessment report (JSON format) identifying vulnerable systems, their current risk level (e.g., "critical_risk", "high_risk", "medium_risk"), and affected components. Example: `{"vulnerable_systems": [{"system_id": "S001", "risk_level": "critical_risk", "affected_components": ["database_server", "web_server"], "threat_match": "T001"}]}`

**Integration:** The system state assessment report is used by Module 4 (Rule-Based Response Recommendation) to determine which systems need protection and by Module 5 (Search-Based Response Recommendation) to understand the current system context when optimizing response sequences.

**Prerequisites:** Requires Module 1's threat detection report as input. No specific AI technique required; this module performs data processing and analysis to assess system vulnerability state. 

---

### Module 4: Rule-Based Response Recommendation

**Topics:** Propositional Logic

**Input:** The threat detection report from Module 1, the threat severity report from Module 2, and the system state assessment report from Module 3. These three inputs together provide complete context about the detected threats, their severity, and the vulnerable systems.

**Output:** A candidate response set (JSON format) containing potential response actions with their associated conditions. Each candidate includes: action type (e.g., "block_ip", "isolate_server", "patch_vulnerability"), target system, trigger conditions, and estimated effectiveness. Example: `{"candidates": [{"action": "block_ip", "target": "192.168.1.100", "condition": "IF threat_type='brute_force' AND severity='high'", "effectiveness": 0.9}]}`

**Integration:** The candidate responses from this module serve as constraints and options for Module 5 (Search-Based Response Recommendation), which explores action sequences using these candidates as the search space. This module's rule-based approach provides quick, explainable recommendations that guide the search optimization.

**Prerequisites:** Course content on Propositional Logic (knowledge bases, inference methods, rule-based reasoning). Requires Modules 1, 2, and 3 outputs as input. 

---

### Module 5: Search-Based Response Recommendation

**Topics:** Search (A*)

**Input:** The candidate response set from Module 4 (JSON format) containing potential response actions. The module uses these candidates as the search space for exploring action sequences.

**Output:** An optimized response action sequence (JSON format) - an ordered list of actions that balance speed of attack mitigation with minimal system cost. Each action in the sequence includes: action type, target, estimated execution time, and cost impact. Example: `{"sequence": [{"action": "block_ip", "target": "192.168.1.100", "order": 1, "time": 2, "cost": 0.1}, {"action": "isolate_server", "target": "S001", "order": 2, "time": 5, "cost": 0.3}]}`

**Integration:** This module produces the final output of the system - the optimized action sequence that security analysts or automated systems can execute. It synthesizes information from all previous modules to provide a comprehensive response plan.

**Prerequisites:** Course content on Search algorithms, specifically A* search with heuristic functions for pathfinding through action state spaces. Requires Module 4's candidate responses as input.


## Feasibility Study

_A timeline showing that each module's prerequisites align with the course schedule. Verify that you are not planning to implement content before it is taught._

| Module | Required Topic(s) | Topic Covered By | Checkpoint Due |
| ------ | ----------------- | ---------------- | -------------- |
| 1      | Propositional Logic | [Check course schedule for when Propositional Logic is taught] | [Checkpoint 1 date] |
| 2      | Machine Learning | [Check course schedule for when Machine Learning is taught] | [Checkpoint 2 date] |
| 3      | Data Processing | No specific AI topic required; can be implemented early | [Checkpoint 2 date] |
| 4      | Propositional Logic | Already covered (used in Module 1) | [Checkpoint 3 date] |
| 5      | Search (A*) | [Check course schedule for when Search algorithms are taught] | [Checkpoint 4 date] |

## Coverage Rationale

The intrusion response domain naturally requires multiple AI techniques working together. Propositional Logic fits threat detection because security threats follow identifiable patterns that can be encoded as logical rules (e.g., "IF failed_login_attempts > threshold AND port = 22 THEN brute_force_attack"). It also fits response recommendation because standard security practices can be captured as rule-based knowledge: matching threat types and severity to appropriate mitigation actions.

Search (A*) is essential for response optimization because incident response is fundamentally a state-space problem. The system must explore sequences of actions (block IP, isolate server, patch vulnerability) while balancing competing objectives: stopping the attack quickly versus minimizing system disruption. A* search with appropriate heuristics can find optimal paths through this action space.

Machine Learning enables severity classification by learning patterns from historical threat data that may not be easily captured in explicit rules. This complements the rule-based detection, handling nuanced cases where threat severity depends on subtle feature combinations.

The main trade-off considered was whether to use Reinforcement Learning for response learning over time. While RL could improve recommendations based on past outcomes, Search provides explainable, immediate optimization which is critical for cybersecurity where analysts need to understand reasoning. The combination of rule-based constraints (Module 4) with search optimization (Module 5) provides both explainability and optimality.
