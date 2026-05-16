# GitHub Repository Mining - Data Mining Report

Generated: 2026-05-11T07:18:45.166996+00:00

## Objective

This project mines GitHub repository data to discover software development trends, influential technologies, common technology stacks, and semantically similar projects.

## Dataset

- Repositories analyzed: 1,000
- Unique technologies/topics: 3,388
- Technology graph edges exported: 1,500
- Data source distribution: {'github_api': 1000}
- Embedding method: BERT/NumPy BERT-Tiny: phob0s/bert-tiny

## Preprocessing

Repository descriptions, README snippets, languages, and topics were cleaned and normalized. Topics were merged with programming languages to create a transaction-style `tech_stack` for each repository.

## Association Rule Mining

Apriori was applied to repository technology stacks. The pipeline exports support, support count, confidence, lift, conviction, and leverage.

| Antecedent | Consequent | Support | Confidence | Lift |
|---|---|---:|---:|---:|
| deep-reinforcement-learning | reinforcement-learning | 0.013 | 0.92857 | 18.57143 |
| deep-reinforcement-learning | machine-learning + reinforcement-learning | 0.013 | 0.92857 | 18.57143 |
| deep-reinforcement-learning + machine-learning | reinforcement-learning | 0.013 | 0.92857 | 18.57143 |
| reinforcement-learning | deep-reinforcement-learning | 0.013 | 0.26 | 18.57143 |
| reinforcement-learning | deep-reinforcement-learning + machine-learning | 0.013 | 0.26 | 18.57143 |
| machine-learning + reinforcement-learning | deep-reinforcement-learning | 0.013 | 0.26 | 18.57143 |
| image-processing | computer-vision + python | 0.013 | 0.54167 | 9.84848 |
| keras | deep-learning + tensorflow | 0.018 | 0.62069 | 9.26402 |
| deep-learning + tensorflow | keras | 0.018 | 0.26866 | 9.26402 |
| keras + python | tensorflow | 0.015 | 0.78947 | 8.39866 |
| keras | python + tensorflow | 0.015 | 0.51724 | 7.83699 |
| keras | tensorflow | 0.02 | 0.68966 | 7.33676 |

## Link Analysis

Technologies are nodes. Weighted edges represent co-occurrence inside repository tech stacks. PageRank identifies central ecosystem technologies, while HITS identifies hub and authority roles.

| Rank | Technology | PageRank | Authority | Hub | Repositories |
|---:|---|---:|---:|---:|---:|
| 1 | machine-learning | 0.07250752 | 0.58336725 | 0.58336725 | 1000 |
| 2 | python | 0.04228662 | 0.48914981 | 0.48914981 | 563 |
| 3 | deep-learning | 0.03083646 | 0.40802086 | 0.40802086 | 400 |
| 4 | artificial-intelligence | 0.01524498 | 0.21472292 | 0.21472292 | 195 |
| 5 | jupyter notebook | 0.01210624 | 0.18050704 | 0.18050704 | 181 |
| 6 | data-science | 0.01200054 | 0.16596141 | 0.16596141 | 143 |
| 7 | pytorch | 0.01152858 | 0.19075133 | 0.19075133 | 145 |
| 8 | computer-vision | 0.00805684 | 0.11701314 | 0.11701314 | 99 |
| 9 | natural-language-processing | 0.00805227 | 0.11267747 | 0.11267747 | 98 |
| 10 | tensorflow | 0.00762683 | 0.12245617 | 0.12245617 | 94 |
| 11 | neural-network | 0.00566841 | 0.09371083 | 0.09371083 | 76 |
| 12 | large-language-model | 0.00423224 | 0.05651513 | 0.05651513 | 50 |

## Semantic/BERT Analysis

Repository text is classified into 11 categories. The default pipeline uses real pretrained BERT-Tiny embeddings through a lightweight NumPy inference path. A SentenceTransformer model can also be supplied with `--semantic-model` when PyTorch is available.

- Average classification confidence: 0.5607
- Largest categories: [('AI/ML Infrastructure', 757), ('Generative AI', 94), ('Data Science', 66), ('Natural Language Processing', 32), ('Mobile Development', 21)]

## Key Insights

- machine-learning is the most central technology by PageRank, appearing in 1000 repositories.
- The strongest association rule is deep-reinforcement-learning -> reinforcement-learning with lift 18.57143 and confidence 0.92857.
- AI/ML Infrastructure is the largest semantic category with 757 repositories.

## Decision Support

The mined rules and graph rankings can be used to recommend technology stacks, identify trending repository domains, and find similar projects for learning or reuse.
