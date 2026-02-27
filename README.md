# Decision Audit System

A systematic tool for auditing, reviewing, and improving past decisions. This system helps individuals and organizations build a structured decision journal, analyze patterns in their decision-making, identify recurring biases, and continuously improve their judgment through evidence-based feedback loops.

## Overview

The most effective way to improve decision-making is to learn from past decisions systematically. The Decision Audit System provides a complete workflow for recording decisions at the time they are made, tracking outcomes over time, and extracting actionable lessons from the comparison. This approach separates decision quality from outcome quality, recognizing that good processes sometimes lead to bad outcomes and vice versa.

This methodology is championed by many of the world's most successful [masters of decision-making](https://keeprule.com/en/masters) who maintain rigorous decision journals and conduct regular reviews of their past choices to refine their judgment.

## Features

- **Decision Journal**: Structured recording of decisions with context and reasoning
- **Outcome Tracker**: Link actual outcomes to past decisions automatically
- **Process Quality Scoring**: Rate decision process independently from outcomes
- **Bias Pattern Detection**: Identify recurring cognitive biases in your decision history
- **Hindsight Analysis**: Separate genuine learning from hindsight bias
- **Calibration Tracking**: Monitor how well confidence levels predict accuracy
- **Team Decision Reviews**: Facilitate structured group decision retrospectives
- **Trend Dashboard**: Visualize decision quality trends over time
- **Automated Reminders**: Schedule follow-ups to review pending decision outcomes
- **Export and Reporting**: Generate comprehensive decision quality reports

## Installation

```bash
pip install decision-audit-system
```

## Quick Start

```python
from das import DecisionJournal, AuditEngine

# Initialize the journal
journal = DecisionJournal(storage="./decisions.db")

# Record a decision at the time it is made
entry = journal.record(
    title="Hire candidate A for senior engineering role",
    context="Three strong candidates interviewed. Team expanding from 8 to 12.",
    alternatives_considered=["Candidate B (more experience)", "Candidate C (lower cost)", "Delay hiring"],
    key_factors=["technical skills", "culture fit", "growth potential", "salary expectations"],
    reasoning="Candidate A showed strongest problem-solving ability and culture alignment despite less experience than B.",
    confidence=0.75,
    expected_outcome="Productive team member within 3 months, strong contributor within 6 months",
    review_date="2024-09-15",
    tags=["hiring", "team_growth", "engineering"]
)

print(f"Decision recorded: {entry.id}")
print(f"Scheduled review: {entry.review_date}")
```

## Core Workflow

### Step 1: Record Decisions

Capture the full context at the time of the decision, before outcomes are known:

```python
from das import DecisionRecord

record = DecisionRecord(
    decision="Switch primary database from PostgreSQL to CockroachDB",
    category="technical_infrastructure",
    stakeholders=["engineering_lead", "dba_team", "cto"],
    information_available=[
        "Current PostgreSQL handling 10K queries/sec",
        "Growth projections suggest 50K queries/sec in 12 months",
        "CockroachDB benchmark shows 3x better horizontal scaling"
    ],
    information_missing=[
        "Long-term CockroachDB stability in production",
        "Team learning curve for new database",
        "Migration risk for existing data"
    ],
    decision_process="consensus",
    time_pressure="moderate",
    reversibility="difficult"
)
```

### Step 2: Track Outcomes

When outcomes become known, record them against the original decision. This practice aligns with fundamental [decision-making principles](https://keeprule.com/en/principles) that emphasize learning from results without falling prey to hindsight bias.

```python
from das import OutcomeTracker

tracker = OutcomeTracker(journal)

tracker.record_outcome(
    decision_id=record.id,
    actual_outcome="Migration completed in 4 months instead of planned 2. Performance improved 2.5x. Two major incidents during migration.",
    outcome_quality=6,  # 1-10 scale
    process_quality=7,  # Separate from outcome
    lessons_learned=[
        "Migration timeline estimates should include 2x buffer",
        "Should have run parallel systems longer",
        "Performance gains validated the technical choice"
    ],
    would_decide_differently=False,
    what_would_change="Longer parallel running period and more conservative timeline"
)
```

### Step 3: Analyze Patterns

Run audits across your decision history to find patterns:

```python
from das import AuditEngine

engine = AuditEngine(journal)

# Run a comprehensive audit
audit = engine.full_audit(timeframe="2024")

print(f"Decisions analyzed: {audit.total_decisions}")
print(f"Average process quality: {audit.avg_process_quality:.1f}/10")
print(f"Average outcome quality: {audit.avg_outcome_quality:.1f}/10")
print(f"Calibration score: {audit.calibration_score:.2f}")
print(f"\nTop biases detected:")
for bias in audit.detected_biases[:5]:
    print(f"  - {bias.name}: {bias.frequency} occurrences ({bias.description})")
```

## Advanced Features

### Bias Detection

The system automatically scans for patterns indicating cognitive biases:

```python
from das import BiasDetector

detector = BiasDetector(journal)
biases = detector.scan(timeframe="last_6_months")

for bias in biases:
    print(f"\nBias: {bias.name}")
    print(f"  Confidence: {bias.confidence:.2f}")
    print(f"  Evidence: {bias.evidence}")
    print(f"  Affected decisions: {len(bias.affected_decisions)}")
    print(f"  Recommendation: {bias.mitigation}")
```

### Calibration Analysis

Track whether your confidence levels accurately predict outcomes across various [decision-making scenarios](https://keeprule.com/en/scenarios):

```python
from das import CalibrationAnalyzer

cal = CalibrationAnalyzer(journal)
report = cal.analyze()

print("Calibration by confidence bucket:")
for bucket in report.buckets:
    print(f"  Stated {bucket.confidence:.0%} confident -> Actually correct {bucket.actual:.0%}")

print(f"\nOverall calibration: {report.overall_score:.2f}")
print(f"Tendency: {report.tendency}")  # "overconfident", "underconfident", or "well-calibrated"
```

### Team Decision Reviews

Facilitate structured retrospectives for team decisions:

```python
from das import TeamReview

review = TeamReview(
    decision_id=record.id,
    participants=["alice", "bob", "charlie"]
)

# Each participant provides independent assessment
review.add_assessment("alice", process_score=7, outcome_score=6, key_lesson="Need more data")
review.add_assessment("bob", process_score=8, outcome_score=5, key_lesson="Timeline was aggressive")
review.add_assessment("charlie", process_score=6, outcome_score=7, key_lesson="Good technical choice")

summary = review.summarize()
print(f"Team consensus process quality: {summary.avg_process:.1f}")
print(f"Agreement level: {summary.agreement_score:.2f}")
print(f"Synthesized lessons: {summary.synthesized_lessons}")
```

## Decision Categories

| Category | Description | Review Frequency |
|----------|-------------|------------------|
| Strategic | Major business direction decisions | Quarterly |
| Technical | Architecture and technology choices | Monthly |
| People | Hiring, promotions, team changes | Semi-annually |
| Financial | Investment and budget allocation | Quarterly |
| Product | Feature prioritization and roadmap | Monthly |
| Operational | Process and workflow changes | Monthly |

For structured templates to guide your audit sessions, the [decision prompts library](https://keeprule.com/en/prompts) offers ready-to-use review frameworks for each decision category.

## Dashboard Metrics

The built-in dashboard tracks key metrics:

- **Decision Volume**: Number of recorded decisions over time
- **Quality Trends**: Process and outcome quality scores over time
- **Calibration Curve**: Visual comparison of confidence vs accuracy
- **Bias Frequency**: Most common biases detected per period
- **Review Completion Rate**: Percentage of decisions with recorded outcomes
- **Improvement Score**: Quantified learning from decision reviews

## Contributing

Contributions are welcome! Areas of interest:

1. Additional bias detection algorithms
2. Integration with project management tools
3. Advanced visualization features
4. Machine learning for pattern detection
5. Mobile companion app development

Fork, branch, and submit a PR with tests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Inspired by the decision journal practices of successful investors and leaders
- Built on research in judgment and decision-making science
- Designed to make systematic decision improvement practical and habitual
