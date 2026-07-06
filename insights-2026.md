# SIGI-2026
## INSIGHTS 

Todor Arnaudov's questions and comments on the paper "Alien space of science ..." and proposals for future work.

https://github.com/alejandrohdez00/alien-space-of-science/issues/1

(...)
Twenkid:

Hi, the file downloaded today! :) Now I can browse the sqlite db, the atoms etc.

```
sqlite3 llm-papers.db 
.schema

CREATE TABLE papers (
    paper_id TEXT PRIMARY KEY,       -- OpenReview note.id
    title TEXT NOT NULL,
    abstract TEXT,
    keywords TEXT,                    -- JSON array as string
    pdf_url TEXT NOT NULL,
    conference TEXT,                  -- Conference key (neurips, iclr, icml)
    venue_year INTEGER NOT NULL,
    venue_track TEXT,
    openreview_url TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
, s2_paper_id TEXT);
CREATE TABLE authors (
    author_id TEXT PRIMARY KEY,      -- Tilde ID (~FirstName_LastName1) or email
    display_name TEXT,
    email TEXT
, s2_author_id TEXT, orcid TEXT);
CREATE TABLE paper_authors (
    paper_id TEXT NOT NULL,
    author_id TEXT NOT NULL,
    author_position INTEGER,         -- 1=first author, 2=second, etc.
    PRIMARY KEY (paper_id, author_id),
    FOREIGN KEY (paper_id) REFERENCES papers(paper_id),
    FOREIGN KEY (author_id) REFERENCES authors(author_id)
);
CREATE INDEX idx_paper_authors_author ON paper_authors(author_id);
CREATE INDEX idx_paper_authors_paper ON paper_authors(paper_id);
CREATE INDEX idx_papers_conference ON papers(conference);
CREATE INDEX idx_papers_year ON papers(venue_year);
CREATE INDEX idx_papers_track ON papers(venue_track);
CREATE INDEX idx_authors_name ON authors(display_name);
CREATE INDEX idx_authors_s2id ON authors(s2_author_id);
CREATE INDEX idx_authors_orcid ON authors(orcid);
CREATE INDEX idx_papers_s2id ON papers(s2_paper_id);
Find papers where "Language" is in the end
sqlite> select title from papers where title like "%language" limit 10
   ...> ;


Learning a Static Analyzer: A Case Study on a Toy Language
Word2net: Deep Representations of Language
WORD SEQUENCE PREDICTION FOR AMHARIC LANGUAGE
Formal Specifications from Natural Language
Socratic Models: Composing Zero-Shot Multimodal Reasoning with Language
Learning Grounded Action Abstractions from Language
Uncovering Gaps in How Humans and LLMs Interpret Subjective Language
Contextualizing biological perturbation experiments through language
ADIFF: Explaining audio difference using natural language
Human-like Few-Shot Learning via Bayesian Reasoning over Natural Language
"Language" can be everywhere:
select title from papers where title like "%language%" limit 10;

Program Synthesis for Character Level Language Modeling
Learning a Static Analyzer: A Case Study on a Toy Language
LSTM-Based System-Call Language Modeling and Ensemble Method for Host-Based Intrusion Detection
Opening the vocabulary of  neural language models with character-level word representations
Data Noising as Smoothing in Neural Network Language Models
Frustratingly Short Attention Spans in Neural Language Modeling
Reference-Aware Language Models
A Neural Knowledge Language Model
Improving Neural Language Models with a Continuous Cache
COLD FUSION: TRAINING SEQ2SEQ MODELS TOGETHER WITH LANGUAGE MODELS
Extract keywords
select DISTINCT j.value from (SELECT keywords from papers limit 100) as x cross join json_each(x.keywords) as j ;
Natural language processing
Deep learning
Computer vision
Theory
Semi-Supervised Learning
Transfer Learning
Sequence-to-Sequence Models
`head -n 50 availability_atoms.json
{
  "0": {
    "text": "A model's reliance on higher-level semantics versus low-level acoustic features can be quantified by 'subtracting' the linear contributions of features like the power spectrum or articulatory characteristics from the model's representations and measuring the remaining alignment with brain activity.",
    "cluster_id": 0,
    "frequency": 23
  },
  "1": {
    "text": "Hardware idle time (computational 'dead time') during large-scale model inference can be minimized by pipelining: fetching model weights for future micro-batches into local memory while simultaneously performing computations on the current batch and writing back the results of previous ones.",
    "cluster_id": 1,
    "frequency": 410
  },
...
unzip -Z1 alien-space-osf-upload-20260515.zip > alien-list.txt
...
alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/ideas.json
alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/blog.md
alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/refined_ideas.json
...
unzip  alien-space-osf-upload-20260515.zip alien-space-osf-upload- 20260515/papers/conf__aaai__PasquierEFTRRS25/ideas.json
Archive:  alien-space-osf-upload-20260515.zip
  inflating: alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/ideas.json  
➜  Downloads head -n 5 alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/ideas.json
{
  "ideas": [
    "Generating multi-instrument sequences as separate, concatenated tracks instead of interleaving events chronologically allows models to treat each instrument as a continuous logical idea, which improves the ability to condition the generation of one instrument on the full context of others.",
    "Infilling missing segments in auto-regressive sequences can be achieved by marking the gap with a placeholder token and moving the generation of the replacement content to the end of the sequence, effectively converting an in-place editing problem into a standard next-token prediction task.",
    "Controllable generation can be implemented by discretizing continuous attribute distributions into ranked 'level tokens' (e.g., dividing note density into ten levels), allowing a user to steer the model by requesting specific relative intensities for different variables.",

unzip  alien-space-osf-upload-20260515.zip alien-space-osf-upload- 20260515/papers/conf__aaai__PasquierEFTRRS25/refined_ideas.json

 head -n 5 alien-space-osf-upload-20260515/papers/conf__aaai__PasquierEFTRRS25/refined_ideas.json

{
  "ratings": [
    {
      "idea": "Generating multi-instrument sequences as separate, concatenated tracks instead of interleaving events chronologically allows models to treat each instrument as a continuous logical idea, which improves the ability to condition the generation of one instrument on the full context of others.",
      "rationale": "The idea clearly contrasts two structural approaches (track-based vs. chronological), explains the mechanism (treating instruments as continuous logical blocks), and states the benefit (improved cross-instrument conditioning). It is fully self-contained and the logic is transferable to other multi-stream sequence tasks.",
```
(...) 
Yes, I find it an interesting resource and food for thought for curious minds and for problems, directions, insights. It is an actual materialization of some of the directions in my hyperbook "The Prophets of the Thinking Machines" - a bigger scale and self-updating "hyper-hyper rolling volume/book" of a survey of AI, and it also can track the developments (time dimensions, slices in time etc.), it may propose future work etc.

A few proposals: the next step which I would do, is:

```
"Idea Atom Nucleus and Electron Clouds"
of
Science
Atoms
Conceptual Units
Everything
Molecules
Macro-Molecules
Cellular organelles ...
1,2,( (3,4,5)|(7,8,9, ..., 6)
```

"Idea Atom Nucleus and Electron Clouds" of Science/Conceptual Units/Everything ...
Finer-grained "tokens" and more explicit "physics" of the transformations for deriving new ones, either higher-level and lower-level.
Changing the resolution, scope. Some of the units may seem "mundane", but they have to be combined in order to produce the complete ones.
(Also deriving how the more recently discovered conceptual units could have been generated from the previous ones and other resources - the literature allows to trace records of some components of the process + implementations and general development of computer science and related fields etc.)
Tools for visualisation and fast travelling through the space and recording the path; one related: Navigu
https://navigu.net/
However in Navigu and similar systems for visual embeddings, the concept of "concept" is reduced to only the label, a word and the connection to the other concepts or clusters in the embedding is not visible or accessible. It should be compositional and structural and derived from previous representations.

Decomposition and combination of constituent parts and also orial break-downs etc., as well as composition into larger units.
Yes, the decomposition and composition are done by the LLMs as well and for generating whole scientific papers, however yet these systems are missing the proper complete granular and transparent "physics" and "mechanics". It is partially enhanced with multimodality, training on structured data, deterministic tools etc. Proper "tools" can replace the whole LLMs.

IMO the end-goal in this domain and the general cognitive machines is everything to be transparent and all derivation of the concepts and actions and all transformations to be observable and traceable even by hand. This is at least my direction - something like the project of an algebra of language and science of Leibniz. His is " Calculus Ratiocinator". One name of mine project is "Zrim" (Зрим - Visible) - Calculus, Algebra, Geometry, an Interpreter/Compiler/Processor etc. of General Intelligence/Thinking/Creativity.

// In my view and in some sense neural networks are in fact also symbolic, but a "perverse" and inefficient "symbolic" system, where even the proper "symbolic" is defined with confused concept - it should be conceptual like the title of your units, and not focused on the "manipulation of symbols"; more on the semantics, the content, affordances - what can be done with the structures, elements ("symbols"), how they can be derived, decomposed, composed etc.

Neural Networks are Also Symbolic: Conceptual Confusions in ANN-Symbolic Terminology, 4.2019
https://www.researchgate.net/publication/403730363_Neural_Networks_are_Also_Symbolic_Conceptual_Confusions_in_ANN-Symbolic_Terminology
....

I'd mention two related works:

Stanislaw Lem's "Summa Technologiae",1964 - "Information Farm" for producing novel scientific discoveries.*
Lem's "farm" is more like the LLMs with "black box" inside the "farm".
IMO the ultimate thinking/scientific machine/processors should generate zero-shot or "first-shot" science and engineering, all output would be correct by design, like produced from an ontology, following basic principles.

Except when it has to be empirically tested in an unclear or unknown domain, where it would be the most innovative, i.e. it doesn't know the specific principles yet.; also the "dead-ends" which the Google Search overview mentions below, are a result of the limitations of the prediction horizon and the precision of the representations.

...

Regarding the space of possible discoveries and the "Alien space", given the landscape of the research literature, I think it is related to the concept from the early Soviet psychology/pedagogy:

Lev Vygotsky, Zone of Proximal Development - https://en.wikipedia.org/wiki/Zone_of_proximal_development
"The zone of proximal development (ZPD) is a concept in educational psychology that represents the space between what a learner is capable of doing unsupported and what the learner cannot do even with support. It is the range where the learner is able to perform, but only with support from a teacher or a peer with more knowledge or expertise."
....

*1. Google Overview: https://www.google.com/search?q=Summa+technologiae+Stanislaw+Lem%27s+information+farm&sca_esv=ec2bff8bd1e2ef21&biw=1551&bih=786&sxsrf=ANbL-n4k8hMt-sLUc2Hs_j_UYFybAs-1lg%3A1781618640409&ei=0FcxaoHEGMOyi-gP2ZC6-Ag&ved=0ahUKEwiB7L7R9ouVAxVD2QIHHVmIDo8Q4dUDCBI&uact=5&oq=Summa+technologiae+Stanislaw+Lem%27s+information+farm&gs_lp=Egxnd3Mtd2l6LXNlcnAiM1N1bW1hIHRlY2hub2xvZ2lhZSBTdGFuaXNsYXcgTGVtJ3MgaW5mb3JtYXRpb24gZmFybTIFEAAY7wUyCBAAGIAEGKIEMgUQABjvBTIIEAAYgAQYogRIwO4BUJ3GAVix6QFwAngBkAEAmAGQAaABgxOqAQQwLjE5uAEDyAEA-AEBmAIOoALdDMICChAAGEcY1gQYsAOYAwCIBgGQBgiSBwQyLjEyoAfMaLIHBDAuMTK4B8wMwgcGMi0xMy4xyAdKgAgB&sclient=gws-wiz-serp

"In Summa Technologiae (1964), Stanisław Lem conceptualized "information farms" as vast, automated computer systems designed to generate, test, and filter entirely new scientific hypotheses without human intervention.
He predicted that these computational networks would eventually outpace human capability, driving the exponential growth of future scientific discovery.
The Concept of the Information FarmIn the "Phantomatics" and "Information Theory" sections of his seminal essay collection, Lem foresaw a future where the sheer volume of scientific data becomes too complex for human minds to synthesize.
An information farm addresses this through: Automated Hypothesis Generation: Massive computational engines that simulate billions of variables and logical permutations to organically "grow" new theories.
Self-Correction and Testing: The farms would continuously run simulated experiments to instantly weed out dead ends, essentially acting as agricultural soil for data. ...
Technological Singularity: Lem recognized that these autonomous systems would eventually produce insights beyond our current biology, accelerating technological evolution faster than human researchers could keep up."

