# ML_quantum_invariant
*Lv Tingrui* 		\<lutingrui745@gmail.com>
## Introduction
This project is targetted at generating invariant predicates for quantum programmes. The basic idea is as follows.
## Basic idea: The modified Code2Inv could be easily and even more efficiently used to generate invariants in Quantum Program

### Review of the classical methods

In the passage [1] the experts in the field have proposed a method to generate loop invariant via the following process:

1. analyse the structure and data of the program, and convert it into a graph, where each element of the program such as operation, judgement and variables are segregated and connected via different types of edges. The edges contain part of the information by acquiring different types, and then convert it into a structured memory.
2. The loop invariant itself is considered as a mini program and set to be of the result of a chain of Markov decision.
3. An attention module which gives attention to different variables of the program.
4. Then they use the reinforcement learning to gain desired properties of the program.

### Why are quantum programmes more suitable?

 As we will see, quantum programs have several advantages which make them more suitable for similar analysis process:

1. Quantum program whether parameterized or not can be easily transformed into an SVTS where each node denotes a position and an edge possess a super-operator, which in itself is a **tensor**[2]. This greatly reduces the complexity of modeling the program to a structured graph since there are no various kind of transitions which cannot be easily modeled. But as quantum program has more capability than traditional program, this may hint that quantum program have more complexity than traditional programs, and we may do the transition between classical and quantum programs when permission and gain more efficiency.
2. The reinforcement learning is easier since the outcome $tr(O[P]\rho)-tr(\Theta\rho)$ is a continuous function[2]. This enables continuous adjustment w.r.t the result.
3. The differentiable programmes of quantum case have been established[3,4], so we can easily acquire the adjustment steps that should be taken be the network.

### General steps

We use the following steps:

1. Encode the quantum program into SVTS control flow graph, and encode the super-operator together with the node from which it begins with. This will encode the full information in a tensor with approximately $n^2$ numbers.
2. Start by arbitrary $O$, and use the Markov chain process to reinforce the outcome. We may use different models. The differentiation theorem mentioned in [3,4] ***may*** be helpful. As mentioned in passage [2], this process will be greatly aimed considering the optimization goal $min(tr(O))$, so we will also add this to the decision process.
3. In the process of learning we may need "attention mode" in [1] as well, but the fact of it shall be discovered by surgical experiments. We may want to give $tr(O)$ a major attention.
4. Parts that can be converted to classical may be assisted by the already exsiting tools.

### To do's

The code of Code2Inv on GitHub[5] seems to be pretty complicated yet versatile so I intend to do some experiments by moving and reconfiguring the code in one git branch.

There are several other optimizations, for example: we may reorder the generation process, starting with the part where the **least** operations are done to one qubit, inspired by [6]. Since the data are very well encoded and do not have order, other ML models than GNNs could be utilized.











---

### Bibliography

[1] Xujie Si, Handgun Day, Mukund Raghothaman, Mayur Naik, and Le Song. 2018. Learning Loop Invariants for Program Verification. In *Advances in Neural Information Processing Systems 31 (NeuIPS)*.

[2] Mingsheng Ying, Shenggang Ying, and Xiaodi Wu. 2017. Invariants of quantum programs: characterisations and generation. In *Proceedings of the 44th ACM SIGPLAN Symposium on Principles of Programming Languages (POPL '17). Association for Computing Machinery, New York, NY, USA, 818–832.* https://doi.org/10.1145/3009837.3009840

[3] Shaopeng Zhu, Shih-Han Hung, Shouvanik Chakrabarti, and Xiaodi Wu. 2020. On the principles of differentiable quantum programming languages. In *Proceedings of the 41st ACM SIGPLAN Conference on Programming Language Design and Implementation (PLDI 2020). Association for Computing Machinery, New York, NY, USA, 272–285.* https://doi.org/10.1145/3385412.3386011

[4] Wang Fang, Mingsheng Ying, Xiaodi Wu. Differentiable Quantum Programming with Unbounded Loops. [arXiv:2211.04507](https://arxiv.org/abs/2211.04507) **[quant-ph]. **https://doi.org/10.48550/arXiv.2211.04507

[5] https://github.com/PL-ML/code2inv?search=1

[6] Hongming Liu, Hongfei Fu, Zhiyong Yu, Jiaxin Song, Guoqiang Li. Scalable Linear Invariant Gener- ation with Farkas’ Lemma. 2022. hal-03463338v2
