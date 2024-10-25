Many methods overlook significance of **considering relations among system components** such as services and users. Understanding these relations is vital for detecting anomalies and their underlying causes. **GLAD is designed to detect relational anomalies in system logs in addition to sequential patterns, structural**. GLAD incorporates log semantics, relational patterns and sequential patterns into a unified framework for anomaly detection.

>[!quote] GNNs are popular for their ability to learn relational pattern



**Basic Idea**
GLAD introduces a field extraction module based on few shot learning to identify essential fields.
Constructs dynamic log graphs for sliding windows by interconnecting extracted fields and log events parsed from log parser.
Utilizes Temporal-attentive graph edge anomaly detection model for anomaly detection. which is GNN based encoder enhanced with transformers to capture content, structural and temporal features.

Each log consist of a _**key template**_ called an **_event**_ and a few variables (known as **_fields_**).
Events placed chronologically forms log sequence.

Pattern Recognition Methods?

**Sequential learning Methods** analyze events sequentially  with a defined sliding window in order to forecast the subsequent event based on the observation window.

However the relation between log events and fields, an essential indicator of system anomalies has often been overlooked. This oversight can lead to missed detection of false alarms, as anomalies may not be apparent from individual events or isolated patterns.

Key Challenges 
- Dynamic graphs need to be built to describe the interactions between log events and fields in different time windows.
- Instead merely detecting anomalies on graph level, we aim to detect anomalous edges representing the relation among nodes which is more challenging task.
- In addition to relational patterns we need to integrate log semantics and sequential patterns as whole for anomaly detection.

Unsupervised Learning which observe only normal event sequence during training has been proven to be more efficient learning paradigm. GLAD focuses on this paradigm. There are supervised learning paradigm too.

$e = {x_1, x_2,...,x_{|e|}}$  log message is a sequence of tokens
$S = {e_1,...,e_{|S|}}$ log sequence is a sequential series of logs
$E = {ent_1,...,ent_{|E|}}$ sequence of entities in a log message
$Y = {l_1,...,l_{|E|}}$  entity labels in a log message
$\mathscr{S} = {S_1,...S_{|S|}}$  total sequences are a set of sequences

Dynamic graph used in GLAD is undirected, attributed, weighted heterogeneous graph.

![[Pasted image 20240318213925.png]]