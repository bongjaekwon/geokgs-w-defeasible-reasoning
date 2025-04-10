# GeoKG-Enabled Similarity Computation with Defeasible Reasoning

## Overview

This repository contains the code, data, and resources for a novel approach to geospatial similarity computation that combines the structured knowledge representation of **GeoKGs** with the flexible inference capabilities of **defeasible logic**. This work addresses the critical need for accurate and interpretable similarity assessments in domains such as urban planning, location-based services, and geographic data integration.

## Key Features

*   **GeoKG Construction:** Integrates data from **OSMnx**, **Wikipedia**, and **GeoNames** to create a rich geospatial knowledge graph.
*   **Defeasible Reasoning:** Employs defeasible logic to reason with incomplete and conflicting information, capturing the uncertainty and context-dependence inherent in spatial similarity judgments.
*   **Rule-Based Similarity:** Represents similarity relationships as defeasible rules based on spatial proximity, shared attributes, and domain knowledge.
*   **Conflict Resolution:** Implements priority-based strategies to resolve conflicts between rules, allowing for nuanced and context-sensitive similarity judgments.
*   **Explainable AI:** Provides transparent and interpretable similarity assessments, offering a valuable alternative to black-box machine learning models.
*   **Benchmarking:** Compares performance against knowledge graph embedding (KGE) models and LLM-based models using an expert-annotated ground truth dataset.
*   **Efficient Computation:** Designed for computational efficiency using techniques like spatial indexing.

## Repository Structure

The repository is organized into the following directories:
├── GeoKG-DR ontology/ # Contains the ontology files defining the GeoKG-DR framework
├── GeoKGsTTL/ # Stores the GeoKG data in RDF/TTL format
├── RawDefeasibleRules/ # Contains the raw defeasible rules generated for reasoning
├── RawGeoJson/ # Includes raw GeoJSON data extracted from OSMnx
└── readme.md # This README file

### Directory Details

1. **GeoKG-DR Ontology**
   - Contains the ontology files used to define the GeoKG-DR framework.
   - The ontology includes classes such as `GeospatialEntity`, `PointOfInterest`, and `SimilarityAssessment`, as well as properties like `nearby`, `hasPriority`, and `similarityScore`.
   - Implemented in OWL and compatible with SPARQL queries.

2. **GeoKGsTTL**
   - Stores the GeoKG data in RDF/TTL format after integrating data from OSMnx, Wikipedia, and GeoNames.
   - Includes spatial geometries, entity types, and relationships represented using GeoSPARQL and Schema.org vocabularies.

3. **RawDefeasibleRules**
   - Contains the raw defeasible rules generated for reasoning.
   - Rules are stored in a text-based format, where each rule consists of an antecedent and a consequent separated by the `=>` symbol.
   - Example:  
     ```
     nearby(e1, e2) ∧ sameType(e1, e2) => similar(e1, e2)
     ```

4. **RawGeoJson**
   - Includes raw GeoJSON data extracted from OSMnx for the study area (Amsterdam).
   - Data includes buildings, roads, points of interest (POIs), and land use polygons.

---

## Methodology

The methodology consists of four main phases:

### 1. GeoKG Construction
- **Data Extraction:** Extracts geospatial features (buildings, roads, POIs, land use) from OSMnx for a specific geographic area (e.g., Amsterdam).
- **Data Integration:** Aligns entities across OSMnx, Wikipedia, and GeoNames based on spatial location and name similarity.
- **Conflict Resolution:** Resolves inconsistencies using a priority order (GeoNames > Wikipedia > OSMnx) and manual review.
- **Knowledge Representation:** Represents entities and relationships in RDF using GeoSPARQL, Schema.org, and custom ontologies.

### 2. Defeasible Rule Generation
- **Rule Templates:** Defines rule templates based on proximity, functional similarity, contextual similarity, and legal/regulatory themes.
- **Rule Instantiation:** Automatically generates rules from templates, populating them with entities and attributes from the GeoKG.
- **Rule Refinement:** Reviews and refines rules with domain experts to ensure accuracy and relevance.

### 3. Reasoning Implementation
- **Reasoning Engine:** Implements a defeasible reasoning engine (adapted from DeReS) to infer similarities based on the generated rules.
- **Rule Encoding:** Encodes defeasible rules in a text-based format compatible with the reasoning engine.
- **Conflict Resolution:** Implements conflict resolution strategies (priority-based, specificity-based) to handle conflicting rules.
- **Similarity Scoring:** Calculates similarity scores based on the inferred conclusions and conflict resolution strategies.

### 4. Experimental Evaluation
- **Ground Truth Dataset:** Creates a ground truth dataset with expert annotations of entity pair similarity scores.
- **Performance Metrics:** Evaluates the approach using precision, recall, F1-score, accuracy, MSE, Spearman correlation, and AUC.
- **Comparative Analysis:** Compares the performance of the defeasible reasoning approach against KGE models and LLM-based models.
- **Explainability Analysis:** Assesses the interpretability and understandability of the defeasible reasoning process.

---

## Results

The experimental results demonstrate the viability of the defeasible reasoning approach for geospatial similarity computation. While KGE models (e.g., ComplEx) achieved higher accuracy (72.3%), the defeasible reasoning approach (67.2%) offers superior interpretability and explainability. An LLM-based model (Gemini) achieved 68.1% accuracy. Rule refinement and conflict resolution strategies significantly impact the performance of the defeasible reasoning approach.

| Model               | Accuracy (%) | Precision | Recall | F1-Score | MSE  | AUC  |
| ------------------- | ------------ | --------- | ------ | -------- | ---- | ---- |
| Defeasible Reasoning | 67.2        | 0.69      | 0.64   | 0.66     | 0.29 | 0.66 |
| KGE (ComplEx)       | 72.3        | 0.75      | 0.68   | 0.71     | 0.22 | 0.73 |
| LLM (Gemini)        | 68.1        | 0.70      | 0.65   | 0.67     | 0.28 | 0.69 |

---

## License
[MIT License]

## Acknowledgements
OSMnx: For providing access to OpenStreetMap data.
Wikipedia: For providing descriptive information about geospatial entities.
GeoNames: For providing basic entity identification and geographic information.
Hugging Face Datasets: For providing the "simeonw/geo_wikipedia_geonames" dataset.
PyKEEN: For providing a framework for training and evaluating KGE models.
Google AI API: For access to the Gemini family of models.

## References

Yan, B., Janowicz, K., Mai, G., & Gao, S. (2017). From ITDL to Place2Vec: Reasoning about place type similarity and relatedness by learning embeddings from augmented spatial contexts. Proceedings of the 25th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems (SIGSPATIAL '17), Article 35, 1–10. https://doi.org/10.1145/3139958.3140054

Koldasbayeva, D., Tregubova, P., Gasanov, M., et al. (2024). Challenges in data-driven geospatial modeling for environmental research and practice. Nature Communications, 15, 10700. https://doi.org/10.1038/s41467-024-55240-8

Cao, K., Zhou, C., Church, R., Li, X., & Li, W. (2024). Revisiting spatial optimization in the era of geospatial big data and GeoAI. International Journal of Applied Earth Observation and Geoinformation, 129, 103832. https://doi.org/10.1016/j.jag.2024.103832

Ihnaini, B., Abuhaija, B., Mills, E. A., & Mahmuddin, M. (2024). Semantic similarity on multimodal data: A comprehensive survey with applications. Journal of King Saud University - Computer and Information Sciences, 36(10), 102263. https://doi.org/10.1016/j.jksuci.2024.102263

Mai, G., Hu, Y., Gao, S., Cai, L., Martins, B., Scholz, J., Gao, J., & Janowicz, K. (2022). Symbolic and subsymbolic GeoAI: Geospatial knowledge graphs and spatially explicit machine learning. Transactions in GIS, 26, 3118–3124. https://doi.org/10.1111/tgis.13012

Lee, W. J., & Lauw, H. W. (2024). Latent representation learning for geospatial entities. ACM Transactions on Spatial Algorithms and Systems, 10(4), Article 32, 31 pages. https://doi.org/10.1145/3663474

Moustafa, A. A. (1989). Architectural representation and meaning: Towards a theory of interpretation (Master's thesis). Massachusetts Institute of Technology, Department of Architecture. http://hdl.handle.net/1721.1/78999

Mai, G., Huang, W., Sun, J., Song, S., Mishra, D., Liu, N., Gao, S., Liu, T., Cong, G., Hu, Y., Cundy, C., Li, Z., Zhu, R., & Lao, N. (2024). On the opportunities and challenges of foundation models for GeoAI (Vision Paper). ACM Transactions on Spatial Algorithms and Systems, 10(2), Article 11, 46 pages. https://doi.org/10.1145/3653070

Delmelle, E. M., Desjardins, M. R., Jung, P., Owusu, C., Lan, Y., Hohl, A., & Dony, C. (2022). Uncertainty in geospatial health: Challenges and opportunities ahead. Annals of Epidemiology, 65, 15–30. https://doi.org/10.1016/j.annepidem.2021.10.002

Lee, J.-G., & Kang, M. (2015). Geospatial big data: Challenges and opportunities. Big Data Research, 2(2), 74–81. https://doi.org/10.1016/j.bdr.2015.01.003

Koons, R. (2022). Defeasible reasoning. In E. N. Zalta (Ed.), The Stanford Encyclopedia of Philosophy (Summer 2022 Edition). Metaphysics Research Lab, Stanford University. https://plato.stanford.edu/archives/sum2022/entries/reasoning-defeasible/

Jiang, B., Wan, G., Xu, J., Li, F., & Wen, H. (2018). Geographic knowledge graph building extracted from multi-sourced heterogeneous data. Acta Geodaetica et Cartographica Sinica, 47(8), 1051–1061. https://doi.org/10.11947/j.AGCS.2018.20180113

Longo, L., Rizzo, L., & Dondio, P. (2021). Examining the modelling capabilities of defeasible argumentation and non-monotonic fuzzy reasoning. Knowledge-Based Systems, 211, 106514. https://doi.org/10.1016/j.knosys.2020.106514

Besnard, P., Moinard, Y., Pereira, W., Clarke, M., & Wilson, N. (1993). DRUMS: Defeasible reasoning and uncertainty management systems. AI Communications, 6(1), 27–46.

Longo, L., Brcic, M., Cabitza, F., Choi, J., Confalonieri, R., Del Ser, J., Guidotti, R., Hayashi, Y., Herrera, F., Holzinger, A., Jiang, R., Khosravi, H., Lecue, F., Malgieri, G., Páez, A., Samek, W., Schneider, J., Speith, T., & Stumpf, S. (2024). Explainable Artificial Intelligence (XAI) 2.0: A manifesto of open challenges and interdisciplinary research directions. Information Fusion, 106, 102301. https://doi.org/10.1016/j.inffus.2024.102301

Diogo, V., Bürgi, M., Debonne, N., Helfenstein, J., Levers, C., Swart, R., & Verburg, P. H. (2023). Geographic similarity analysis for Land System Science: Opportunities and tools to facilitate knowledge integration and transfer. Journal of Land Use Science, 18(1), 227–248. https://doi.org/10.1080/1747423X.2023.2218372

Antonelli, A. G. (2004). Logic. In L. Floridi (Ed.), The Blackwell Guide to the Philosophy of Computing and Information. https://doi.org/10.1002/9780470757017.ch20

Billington, D. (2008). Propositional clausal defeasible logic. In S. Hölldobler, C. Lutz, & H. Wansing (Eds.), Logics in Artificial Intelligence. JELIA 2008 (Lecture Notes in Computer Science, vol. 5293). Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-87803-2_5

Andrews, R. (2003). An automated rule refinement system (PhD thesis). Queensland University of Technology. https://eprints.qut.edu.au/15788/

Dash, T., Chitlangia, S., Ahuja, A., et al. (2022). A review of some techniques for inclusion of domain-knowledge into deep neural networks. Scientific Reports, 12, 1040. https://doi.org/10.1038/s41598-021-04590-0

Li, Q., Li, Y., Gao, J., Zhao, B., Fan, W., & Han, J. (2014). Resolving conflicts in heterogeneous data by truth discovery and source reliability estimation. In Proceedings of the 2014 ACM SIGMOD International Conference on Management of Data (SIGMOD '14) (pp. 1187–1198). Association for Computing Machinery. https://doi.org/10.1145/2588555.2610509

Mai, G., Xie, Y., Jia, X., Lao, N., Rao, J., Zhu, Q., Liu, Z., Chiang, Y.-Y., & Jiao, J. (2025). Towards the next generation of Geospatial Artificial Intelligence. International Journal of Applied Earth Observation and Geoinformation, 136, 104368. https://doi.org/10.1016/j.jag.2025.104368

Tian, L., Zhou, X., Wu, Y.-P., Zhou, W.-T., Zhang, J.-H., & Zhang, T.-S. (2022). Knowledge graph and knowledge reasoning: A systematic review. Journal of Electronic Science and Technology, 20(2), 100159. https://doi.org/10.1016/j.jnlest.2022.100159

Lv, X., Gu, Y., Han, X., Hou, L., Li, J., & Liu, Z. (2019). Adapting meta knowledge graph information for multi-hop reasoning over few-shot relations. In Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP) (pp. 3376–3381). Association for Computational Linguistics.

Xian, Y., Fu, Z., Muthukrishnan, S., de Melo, G., & Zhang, Y. (2019). Reinforcement knowledge graph reasoning for explainable recommendation. In Proceedings of the 42nd International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR'19) (pp. 285–294). Association for Computing Machinery. https://doi.org/10.1145/3331184.3331203

Chen, J., Deng, S., & Chen, H. (2017). CrowdGeoKG: Crowdsourced Geo-Knowledge Graph. In J. Li, M. Zhou, G. Qi, N. Lao, T. Ruan, & J. Du (Eds.), Knowledge Graph and Semantic Computing. Language, Knowledge, and Intelligence. CCKS 2017 (Communications in Computer and Information Science, vol. 784). Springer, Singapore. https://doi.org/10.1007/978-981-10-7359-5_17

Nute, D. (2003). Defeasible logic. In O. Bartenstein, U. Geske, M. Hannebauer, & O. Yoshie (Eds.), Web Knowledge Management and Decision Support. INAP 2001 (Lecture Notes in Computer Science, vol. 2543). Springer, Berlin, Heidelberg. https://doi.org/10.1007/3-540-36524-9_13

Delrieux, C. (2004). Abductive inference in defeasible reasoning: A model for research programmes. Journal of Applied Logic, 2(4), 409–437. https://doi.org/10.1016/j.jal.2004.07.003

Dai, X. L., Zhu, Y. Q., Yang, J., et al. (2022). Research and implementation of geospatial data similarity calculation method. Journal of Global Change Data & Discovery, 6(4), 501–512. https://doi.org/10.3974/geodp.2022.04.01

Schwering, A. (2008). Approaches to semantic similarity measurement for geo-spatial data: A survey. Transactions in GIS, 12, 5–29. https://doi.org/10.1111/j.1467-9671.2008.01084.x

Xiao, J., & He, Z. (2017). A novel approach to semantic similarity measurement based on a weighted concept lattice: Exemplifying geo-information. ISPRS International Journal of Geo-Information, 6(11), 348. https://doi.org/10.3390/ijgi6110348

van Kreveld, M., Miltzow, T., Ophelders, T., Sonke, W., & Vermeulen, J. L. (2022). Between shapes, using the Hausdorff distance. Computational Geometry, 100, 101817. https://doi.org/10.1016/j.comgeo.2021.101817

Rodriguez, M. A., & Egenhofer, M. J. (2003). Determining semantic similarity among entity classes from different ontologies. IEEE Transactions on Knowledge and Data Engineering, 15(2), 442–456. https://doi.org/10.1109/TKDE.2003.1185844

Bordes, A., Usunier, N., Garcia-Durán, A., Weston, J., & Yakhnenko, O. (2013). Translating embeddings for modeling multi-relational data. In Proceedings of the 27th International Conference on Neural Information Processing Systems - Volume 2 (NIPS'13) (Vol. 2, pp. 2787–2795). Curran Associates Inc.

Guo, S., Wang, Q., Wang, L., Wang, B., & Guo, L. (2016). Jointly embedding knowledge graphs and logical rules. In Proceedings of the 2016 Conference on Empirical Methods in Natural Language Processing (pp. 192–202). Association for Computational Linguistics.

Das, R., Dhuliawala, S., Zaheer, M., Vilnis, L., Durugkar, I., Krishnamurthy, A., Smola, A., & McCallum, A. (2018). Go for a walk and arrive at the answer: Reasoning over paths in knowledge bases using reinforcement learning. arXiv:1711.05851 [cs.CL]. https://doi.org/10.48550/arXiv.1711.05851

Bassiliades, N., Antoniou, G., & Governatori, G. (2007). Proof explanation in the DR-DEVICE system. In Web Reasoning and Rule Systems. RR 2007. Lecture Notes in Computer Science, vol 4524 (pp. 273–286). Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-540-72982-2_19

Bryant, D., & Krause, P. (2008). A review of current defeasible reasoning implementations. The Knowledge Engineering Review, 23(3), 227–260. https://doi.org/10.1017/S0269888908001318

Kravari, K., Papatheodorou, I., & Bessis, N. (2010). A survey of reasoning techniques for agent-based systems. Computational and Mathematical Organization Theory, 16(3), 255–282. https://doi.org/10.1007/s10588-010-9073-0

Stoutenburg, S., Obrst, L., Nichols, D., Samuel, K., & Franklin, P. (2006). Applying semantic rules to achieve dynamic service-oriented architectures. In Proceedings of the 2006 IEEE International Symposium on Rule Interchange and Application (RuleML 2006) (pp. 75-82). https://doi.org/10.1109/RULEML.2006.4

Powers, D., & Ailab, (2011). Evaluation: From precision, recall and F-measure to ROC, informedness, markedness & correlation. Journal of Machine Learning Technology, 2, 2229-3981. https://doi.org/10.9735/2229-3981

Rizzo, L., & Longo, L. (2018). A qualitative investigation of the degree of explainability of defeasible argumentation and non-monotonic fuzzy reasoning. In Proceedings of the 26th AIAI Irish Conference on Artificial Intelligence and Cognitive Science (pp. 138-149). https://doi.org/10.21427/tby8-8z04

Simeonw. (2025). Geo-Wikipedia-GeoNames Dataset. https://huggingface.co/datasets/simeonw/geo_wikipedia_geonames

Cholewinski, P., Marek, V. W., & Truszczynski, M. (1996). Default reasoning system DeReS. In Proceedings of the Fifth International Conference on Principles of Knowledge Representation and Reasoning (KR'96) (pp. 518–528). Morgan Kaufmann Publishers Inc., San Francisco, CA, USA.

Ali, M., Berrendorf, M., Hoyt, C. T., Vermue, L., Sharifzadeh, S., Tresp, V., & Lehmann, J. (2021). PyKEEN 1.0: A Python Library for Training and Evaluating Knowledge Graph Embeddings. Journal of Machine Learning Research, 22(82), 1–6. http://jmlr.org/papers/v22/20-825.html

Anil, R., Borgeaud, S., Alayrac, J.-B., Yu, J., Soricut, R., Schalkwyk, J., Dai, A. M., Hauth, A., Millican, K., Silver, D., Johnson, M., et al. (2023). Gemini: A Family of Highly Capable Multimodal Models. arXiv:2312.11805 [cs.CL]. https://doi.org/10.48550/arXiv.2312.11805
