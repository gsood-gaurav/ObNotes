
Fine-tuning large pretrained models in an effective transfer mechanism in NLP. However in presence of many downstream tasks fine tuning is [[parameter inefficient]], an entire new model is required for every task. As an alternative, we propose transfer with adapter modules. Adapter modules yield compact and extensible model; they add only few trainable parameters per task and new tasks can be added without revisiting previous ones. The parameter of original network remain fixed, yielding high degree of parameter sharing.

> BERT transferred with adapters 26 diverse text classification tasks including GLUE and other tasks attains near state of the art performance whilst adding few parameters per task. On GLUE we obtain with 0.4 % of the performance of full fine tuning adding only 3.6% parameters per task. By contrast full fine tuning trains 100% of parameters per task.

![[Pasted image 20240327193513.png]]

In this paper we address online setting, where tasks arrive in stream. The goal is to build a system that perform well on all of them, but without training an entire new model for every new task. A high degree of sharing between tasks is particulary useful for applications such as cloud services where models need to solve many tasks that arrive from customers in sequence. For this we propose a transfer learning strategy that yields a compact and extensible downstream models.

**Two most common transfer learning techniques in NLP are feature-based transfer and fine-tuning**
Feature based techniques often works poorer as compared to fine tuning. Both feature-based transfer and fine-tuning require a new set of weights for each task. Fine tuning is more parameter efficient if lower layers of the network are shared among tasks.

![[Pasted image 20240327195612.png]]

