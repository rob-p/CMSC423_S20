---
layout: page
title: Course Materials
permalink: /course-materials/
---

<!--{% include image.html url="/_images/cover2.jpg" width=175 align="right" %}-->

# Syllabus for CMSC423: Bioinformatics Algorithms, Databases, and Tools

Here you'll find an overview of the course — the material I expect we'll cover, the breakdown of course assignments and credit, and the course policies.

## Logistics

* Course Website : [https://rob-p.github.io/CMSC423_S20/](https://rob-p.github.io/CMSC423_S20/)
* Instructor : Rob Patro
* Instructor office hours: Tuesdays 1-2PM in IRB 3220, or by appointment
* Class location: IRB 0318
* Class days/time: Tuesdays/Thursdays 11:00 AM — 12:15 PM
* TAs : 
  - Yuelin Liu (yuelin@cs.umd.edu)
    - Office hours : Tues. 4-5PM across from IRB 5138
  - Hadi Yami (hadiyami@cs.umd.edu) Office hours to be posted later this week
    - Office hours : Wed. 4-5PM across from IRB 5138
  
## Course Content

**Links**: 

 * In general, _this website_ is the place to look for course content and course news.  Any content that is private / restricted (e.g. grades) will be made available on the ELMS page for this course.  Additionally, you should register on both Project Rosalind and Piazza for this course (links below).

 * Assignment announcements and deadlines will be posted on the [ELMS page for this course](https://umd.instructure.com/courses/1275340), and grading information will be made available there.
 
 * The small programming assignments will be turned in via Project Rosalind.  Please use [this link](http://rosalind.info/classes/enroll/a7d62f0502/) to enroll in this session of the course on Rosalind.

 * The course also has a Piazza page for discussions.  Please register for this course on Piazza [here](http://www.piazza.com/umd/spring2020/cmsc423).

**Textbook(s)**: The book for this course is [Bioinformatics Algorithms: An Active Learning Approach](https://secure.mybookorders.com/Orderpage/1402). [The website for the book](http://bioinformaticsalgorithms.com/index.htm) contains other helpful information as well. Further resources, where relevant, will be provided via links on the course website accompanying the slides or lecture notes. However, as this is an _upper-level_ course, and you should _absolutely_ seek out other sources explaining these topics from different angles, using different notations and examples, etc.  Of course, you should also _absolutely_ reach out to the TAs and me if you are having trouble understanding a topic in the course and have been unable to become comfortable with it from the lecture slides and other sources.  In addition
to the required text, here are some (non-required) textbooks that I personally recommend as references for different topics:

**Genomics algorithms, data structures, and statisitcal models**:

- [Genome Scale Algorithm Design](http://www.cs.helsinki.fi/group/gsa/book/) (Mäkinen, Belazzougui, Cunial, Tomescu 2015)
- [Biological Sequence Analysis](http://www.amazon.com/Biological-Sequence-Analysis-Probabilistic-Proteins/dp/0521629713) (Durbin, Eddy, Krogh, Mitchinson 1998)

**Basics of algorithms and data structures**:

This course will assume familiarity with basic algorithms and data structures, though I will attempt to refresh everyone's memory on
relevant concepts when we cover them.  If you need a refresher on algorithmic basics, I recommend the following resources:

- [Algorithms](http://algorithmics.lsi.upc.edu/docs/Dasgupta-Papadimitriou-Vazirani.pdf) (Dasgupta, Papadimitriou, and Vazirani 2006)
- [Algorithm Design](http://www.amazon.com/Algorithm-Design-Jon-Kleinberg/dp/0321295358) (Kleinberg and Tardos 2006)
- [Introduction to Algorithms, 3rd edition](https://www.amazon.com/Introduction-Algorithms-3rd-MIT-Press/dp/0262033844)(Cormen, Leiserson, Rivest and Stein, 2009)

**Molecular biology**:

We will cover the basic required molecular Biology in the course. However if you're not familiar with basic molecular Biology, there are some useful resources worth reading:

- [Molecular Biology of the Cell](http://www.ncbi.nlm.nih.gov/books/bv.fcgi?call=bv.View..ShowTOC&rid=mboc4.TOC&depth=2) (Alberts,  Johnson,  Lewis,  Raff,  Roberts and  Walter, 2002)
- [Molecular Biology: Principles of Genome Function 2nd Edition](https://www.amazon.com/Molecular-Biology-Principles-Genome-Function/dp/0198705972/) (Craig,  Green, Greider, Storz, Wolberger, Cohen-Fix, 2014)
- [Molecular Biology](http://www.amazon.com/Molecular-Biology-Second-Edition-David/dp/0123785944) (Clark and Pazdernik 2012)

**Expectations**: Since this is a computational biology course, you will be expected to become familiar with the relevant biology — it is an important and inextricable part of the material, and the underlying biology provides motivation for the computational problems we will tackle.  However, as an upper-level computer science course, our focus will be on the computational aspects of bioinformatics and genomics.  It is expected that you enter the class with a strong understanding of algorithms and basic data structures, and that you leave the class with a knowledge of how algorithm and data structure design can be fruitfully applied to biological data. 

## Course Objectives

The main objective of this course will be to provide an understanding of some of the algorithms, data structures, and statistical methods that underlie _modern_ computational genomics. This course is intended as a broad introduction to bioinformatics and computational biology.  However, this is a huge field, so we will not cover everything, and what we do cover will not all be at the same depth (e.g. we will spend more time discussing indexing than clustering).   Our perspective will be a computational and algorithmic one, though we will take the time to understand the necessary biology and motivation for the problems we discuss. At the end of this course, you should have a good understanding of how new challenges in genomics drive algorithmic innovations and how algorithmic innovations enable new and improved biological analyses.


## Course  Schedule

The following is a planned schedule of the material we will cover in the course, as well as when we will cover it.  The mapping between content and dates below _is subject to change_ depending on how quickly we move.  The current schedule is  optimistic, and I would like to cover all of this material.  However, it's much more important that the class understand the material we cover than that we get to all of the topics I'd like to discuss.  Thus, the time we spend on certain topics and the precise list of topics we cover is subject to change throughout the semester depending on our pace.

- Week of Jan 27.
  - Course introduction, logistics & goals
  - Overview of bioinformatics, basic biology & biotechnology

- Week of Feb 3. (P&C Chapter 1)
  - Exact string matching
  - KMP & Z algorithms
  - **Note** : February 7 : Last day to drop without a `W`
  
- Week of Feb 10. (P&C Chapter 9)
  - Text indexing for rapid search (overview & Suffix Trie)
  
- Week of Feb 17. 
  - Suffix Arrays
  - BWT and FM-index
  
- Week of Feb 24.
  - Feb 25. : Midterm 1 (in class)
  - Feb 27. : Prof. Patro out of town
  
- Week of March 2. (P&C Chapter 5)
  - Sequence alignment & dynamic programming
  - March 5 : Prof. Patro out of town

- Week of March 9.
  - Sequence alignment continued (local and semi-local variants) & linear space
  
- Week of March 16 **Spring Break, no classes**

- Week of March 23 (P&C Chapter 2)
  - Motif finding & Gibbs sampling
  - Probabilistic sequence modeling 

- Week of March 30 (P&C Chapter 8)
  - Clustering (hierarchical & k-means)
  
- Week of April 6
  - April 9 : Midterm 2 (in class)
  - April 11 : Last day to drop with a `W`
 
- Week of April 13 
  - RNA-sequencing and estimating gene expression
  - More probabilistic modeling (sufficient statistics)
  
- Week of April 20 (P&C Chapter 7)
  - Phylogenomics, parsimony (small) and maximum likelihood 
  
- Week of April 27 (P&C Chapter 3)
  - Phylogenomics continued
  - Genome assembly & the de Bruijn graph
  
- Week of May 4 
  - Genome assembly and the de Bruijn graph continued
  - May 7 : Prof. Patro out of town (_tentative_, will verify)

- Week of May 11 
  - Wrap-up and current research topics in computational biology
  - May 12 : Last day of class

- May 14 : Final Exam (8:00-10:00am) **Note: University assigned time different than class time**

## Course Resources

The course website is [https://rob-p.github.io/CMSC423_S20/](https://rob-p.github.io/CMSC423_S20/), which is probably where you are reading this right now.

The course has a Piazza page, and you can enroll [here](https://piazza.com/umd/spring2020/cmsc423).  I encourage you to interact with each other, raise questions, and discuss course topics using Piazza.  This is also the best place to raise general questions about material we cover in the course (as opposed to e.g. an e-mail), since other students can see the response and ask follow-up questions.  This helps to reduce redundancy in the answering of questions.

Assignments will be posted and collected [via ELMS](https://umd.instructure.com/courses/1275340).

## Course Policies

**Coursework and grading**: The coursework will consist of small programming assignments, a couple of larger
projects, a midterm exam and a final exam. The breakdown of weights for these different assignments will be as follows:

- Homeworks & short prgramming assignments — 15%
- Projects - 25%
- Midterm 1 - 15%
- Midterm 2 - 15%
- Final Exam — 30%

**Late policy**: Assignments that are turned in late will be docked 1% for each hour they are late up to the first 48 hours.  After 48 hours, late assignments will not be accepted.

**Regrade policy**: All requests to re-grade, re-check, or re-mark an assignment or exam question **must be made in writing**. When the assignment is re-graded, it will be re-checked in its entirety. This means that *it is possible to lose points on other problems if they were graded incorrectly or too leniently the first time*. Therefore, I urge you to thoroughly consider each regrade request you make.

**Excused Absences**: If you miss a class for a medical or health-related reason, please provide me with a record of this in writing or via e-mail (I do not need to know the specifics, just the date of your absence and that it was for a medical or health reason). If, for a health-related or medical reason, you will miss two or more consecutive classes, or will miss class on a recurring basis, or were unable to meet a particular academic obligation of this course, I will require a written note from the Student Health Service or a healthcare provider documenting the range of dates for which you were unable to meet your academic obligations. This note need not contain any diagnostic information. If you will miss any classes or scheduled exams as a result of religious observances, you must submit this information to me, in writing, within the first two weeks of the semester to make necessary accommodations to complete the work that will be missed.

**Final Grades**: The grade you receive in this class will reflect, as much as possible, the degree to which you have mastered the necessary material. How much somebody “needs” an ‘A’ will have no bearing on whether or not (s)he receives an ‘A’, other than how this need or desire is reflected in the work that (s)he does. I want everyone to do well in this course, and will make every reasonable effort to help you understand the material as well as possible. However, barring errors in the grading of assignments, the grades you receive at the end of the semester are final, and I will not alter them for personal or non-academic reasons, *so please do not ask me to*!

**Academic integrity**: 

*TLDR* : Don't cheat.  Don't copy code from friends, classmates, or the internet for the short programming assignments or the projects. Don't provide code to classmates for any of the assignments or projects.  Don't cheat on the exams.  Be cool, and everything will be cool.

*Long form* : [From the University's Undergraduate Catalog Statement on Academic Integrity ](https://academiccatalog.umd.edu/undergraduate/registration-academic-requirements-regulations/academic-integrity-student-conduct-codes/):

> The University of Maryland is an academic community. Its fundamental purpose is the pursuit of knowledge. Like all other communities, the University can function properly only if its members adhere to clearly established goals and values. Essential to the fundamental purpose of the University is the commitment to the principles of truth and academic honesty. Accordingly, the Code of Academic Integrity is designed to ensure that the principle of academic honesty is upheld. While all members of the University share this responsibility, the Code of Academic Integrity is designed so that special responsibility for upholding the principle of academic honesty lies with the students.

> The University's Code of Academic Integrity is a nationally recognized honor code, administered by a Student Honor Council. Any of the following acts, when committed by a student, shall constitute academic dishonesty:

 * Cheating: fraud, deceit, or dishonesty in any academic course or exercise in an attempt to gain an unfair advantage and/or intentionally using or attempting to use unauthorized materials, information, or study aids in any academic course or exercise.
 
 * Fabrication: intentional and unauthorized falsification or invention of any information or citation in any academic course or exercise.

 * Facilitating academic dishonesty: Intentionally or knowingly helping or attempting to help another to violate any provision of the Code of Academic Integrity.
 
 * Plagiarism: Intentionally or knowingly representing the words or ideas of another as one's own in any academic course or exercise.
 
> If it is determined that an act of academic dishonesty has occurred, a grade of "XF" is considered the normal sanction for undergraduate students. The grade of "XF" is noted on the academic transcript as failure due to academic dishonesty. Lesser or more severe sanctions may be imposed when there are circumstances to warrant such consideration. Suspension or expulsion from the University may be imposed even for a first offense.

Academic integrity is a very serious issue. Any assignment, project or exam you complete in this course is expected to be your own work. If you are allowed to discuss the details of or work together on an assignment, this will be made explicit. Otherwise, you are expected to complete the work yourself. *Plagarism is not just the outright copying of content*. If you paraphrase someone else's thoughts, words, or ideas and you don't cite your source, this constitues plagraism. It is always much better to turn in an incorrect or incomplete assignment representing your own efforts than to attempt to pass off the work of another as your own. **If you are academically dishonest in this course, you will recieve a grade of XF, and you will be reported to the university's Office of Student Conduct**.

## Academic Accommodations:

This course adopts the following policy from the CMSC Course Administration Guide:

### Accessibility and Disability Service, ADS

Any student eligible for and requesting reasonable academic accommodations due to a disability is requested to provide, to the instructor in office hours, a letter of accommodation from the Office of Accessibility and Disability Services (ADS) within the first two weeks of the semester. If for some reason ADS accommodation is only granted to a student mid-semester, it applies to coursework from then on, not retroactively.

### Excused Absences

Any student who needs to be excused for an absence from a single lecture, recitation, or lab due to a medically necessitated absence shall make a reasonable attempt to inform the instructor of his/her illness prior to the class. Upon returning to the class, present their instructor with a self-signed note attesting to the date of their illness.  Each note must contain an acknowledgment by the student that the information provided is true and correct.  Providing false information to University officials is prohibited under Part 9(i) of the Code of Student Conduct (V-1.00(B) University of Maryland Code of Student Conduct) and may result in disciplinary action.

Self-documentation may not be used for major grading events (e.g., exams, project deadlines, etc.).  Any student who needs to be excused for a prolonged absence (2 or more consecutive class meetings), or for a Major Scheduled Grading Event, must provide written documentation of the illness from the Health Center or from an outside health care provider. This documentation must verify dates of treatment and indicate the timeframe that the student was unable to meet academic responsibilities. In addition, it must contain the name and phone number of the medical service provider to be used if verification is needed. No diagnostic information will ever be requested.

### Accomodations for religious reasons

In general, students must request accommodations for religious reasons during the first two weeks of classes.  In this course, this applies mostly to notifying me about expected absences from class.  The homeworks and projects are assigned far-enough in advance that it is not reasonable that extensions or delays be provided for religious reasons.
