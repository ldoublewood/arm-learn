# [2508.05415] Do Robots Really Need Anthropomorphic Hands?

\[1\]\\fnmAlexander \\surFabisch

\[1\]\\orgdivRobotics Innovation Center, \\orgnameDeutsches Forschungszentrum für Künstliche Intelligenz GmbH (DFKI), \\orgaddress\\streetRobert-Hooke-Straße 1, \\cityBremen, \\postcode28359, \\stateBremen, \\countryGermany

2\]\\orgdiv[L3S Research Center](https://www.l3s.de/), \\orgnameLeibniz Universität Hannover, \\orgaddress\\streetAppelstraße, \\cityHanover, \\postcode30167, \\stateLower Saxony, \\countryGermany

###### Abstract

Human manipulation skills represent a pinnacle of their voluntary motor functions, requiring the coordination of many degrees of freedom and processing of high-dimensional sensor input to achieve such a high level of dexterity. Thus, we set out to answer whether the human hand, with its associated biomechanical properties, sensors, and control mechanisms, is an ideal that we should strive for in robotics—do we really need anthropomorphic robotic hands?

This survey can help practitioners to make the trade-off between hand complexity and potential manipulation skills. We provide an overview of the human hand, a comparison of commercially available robotic and prosthetic hands, and a systematic review of hand mechanisms and skills that they are capable of. This leads to follow-up questions. What is the minimum requirement for mechanisms and sensors to implement most skills that a robot needs? What is missing to reach human-level dexterity? Can we improve upon human dexterity?

Although complex five-fingered hands are often used as the ultimate goal for robotic manipulators, they are not necessary for all tasks. We found that wrist flexibility and finger abduction/adduction are important for manipulation capabilities. On the contrary, increasing the number of fingers, actuators, or degrees of freedom is often not necessary. Three fingers are a good compromise between simplicity and dexterity. Non-anthropomorphic hand designs with two opposing pairs of fingers or human hands with six fingers can further increase dexterity, suggesting that the human hand may not be the optimum.

###### keywords: 

Robotics Hands, Grippers, Smart Prosthetics, Manipulation, Grasping 

## 1 Introduction

The human hand is often used as the gold standard or goal for robotic manipulation and haptic perception. Robots with anthropomorphic hands that are capable of complex manipulation skills are often used to illustrate sophisticated robotics and artificial intelligence.

However, despite our fascination for anthropomorphic robotic hands, the trend in industrial applications and robotic challenges is to use simpler designs consisting of parallel grippers or suction cups. This trend is not necessarily only due to the complexity of matching the human hand’s dexterity, robustness, and perceptual capabilities, but perhaps also to the reality that anthropomorphic hands might not be required to manipulate efficiently. For instance, the winner of the Amazon Picking Challenge used an end effector based on a suction system \[[75](#bib.bib75)\]. In the DARPA Robotics Challenge, 15 of 25 teams used an underactuated hand with three or four fingers, while none of the remaining ten teams used a fully actuated anthropomorphic hand \[[75](#bib.bib75)\]. This trend is also observed in assistive technologies, e.g., in the Cybathlon, which is a global challenge organized by ETH Zurich to develop assistive technologies suitable for everyday use for people with disabilities: the winner of the Powered Arm Prosthesis Race used a body-powered hook \[[75](#bib.bib75)\]. Furthermore, birds are often able to perform complex manipulations, such as nest building, just with their beaks \[[95](#bib.bib95)\].

In contrast to these observations, we can see that humans often use more than one hand with five fingers to solve complex manipulation tasks, e.g., tying shoe laces. This observation suggests that having only one opposable thumb and five fingers may not be sufficient for solving this task. This hypothesis is supported by the fact that there are people with six-fingered hands who can tie shoe laces with just one of their hands and achieve superior manipulation abilities in several other tasks \[[59](#bib.bib59)\]. When we design new robotic hands from scratch, we could improve the dexterity, flexibility, and versatility of the mechanism, for instance, by introducing two opposable thumbs or six fingers \[[8](#bib.bib8)\].

All of which prompts the question of whether we need anthropomorphic robotic hands. Attempting to answer this question, we analyze the human hand and its capabilities, including kinematics and perception, to find characteristic features of anthropomorphic hands. Furthermore, we review commercially available robotic and prosthetic hands to identify anthropomorphic features that are technically feasible. Then we perform a systematic literature review to correlate hand features derived from the previous two sections, skill categories, and manipulable degrees of freedom. We conclude with a discussion that connects our findings to literature from neuroscience, biology, prosthetics, and robotics.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x1.png) 

Figure 1: Kinematics of the human hand (legend in Figure [7(a)](#S3.F7.sf1 "In Figure 7 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?")).

## 2 The Human Hand

To answer whether robotic hands need to be more like human hands, we define the characteristics of the human hand in terms of biomechanics, sensors, control, and learning.

### 2.1 Biomechanics of the Human Hand

The human hand is one of the most advanced manipulation devices that can be found in nature \[[41](#bib.bib41)\].

#### 2.1.1 Joints and Degrees of Freedom

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig2.jpeg) 

Figure 2: Bones of the human hand. Image from \[[118](#bib.bib118)\] CC BY 4.0\. Fingers are enumerated from thumb (1) to little finger (5).

The human hand has many bones (see Figure [2](#S2.F2 "Figure 2 ‣ 2.1.1 Joints and Degrees of Freedom ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?")), but not all of them are connected through movable joints. The human hand has 20 undeniable degrees of freedom—four in each finger. Index, middle, ring, and little finger can perform flexion and extension in three joints (metacarpo-phalangeal joint, MCP; proximal interphalangeal joint, PIP; distal interphalangeal joint, DIP) and adduction (moving closer to the middle finger) and abduction (moving away from the middle finger) in one joint (MCP). The thumb is a special case with a saddle joint (trapezo-metacarpal joint, TMC) that has two degrees of freedom to achieve flexion/extension and opposition/reposition, and two more joints (MCP and interphalangeal joint, IP) to perform flexion/extension. It is possible to move the metacarpal bones and hollow the palm to a limited extent \[[41](#bib.bib41)\] so that \[[15](#bib.bib15)\] define hand kinematics with 24 degree of freedom. Assuming the carpus to be rigid is only an approximation \[[41](#bib.bib41)\], and the palm, as well as the skin, are soft and deformable. A kinematic diagram of the hand is displayed in Figure [1](#S1.F1 "Figure 1 ‣ 1 Introduction ‣ Do Robots Really Need Anthropomorphic Hands?").

#### 2.1.2 Range of Motion

Cobos et al. \[[15](#bib.bib15), Table III\] provide a concise overview of the range of motion for each joint.111Range of flexion seems to be swapped between MCP and PIP joints \[[41](#bib.bib41)\]. However, the exact range depends on the person. For example, a human can have distal hyperextensibility of the thumb (hitchhiker’s thumb), which allows them to extend their thumb’s IP joint by 90 degrees so that its active range of motion is 180 degrees. The Kapandji index \[[40](#bib.bib40)\] measures the range of motion of opposition/reposition in the thumb’s TMC joint to evaluate an individual’s dexterity. Furthermore, there is a range that can be actively reached through muscle contraction and it is possible to extend movement in some joints even further through contact with the environment. For example, passive extension in the DIP joints can be about 30 degrees \[[41](#bib.bib41)\], which is considerably larger than the active extension of 5 degrees.

#### 2.1.3 Muscles and Tendons

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig3a.jpeg) 

(a) Muscles in the forearm move the wrist, hand, and fingers.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig3b.jpeg) 

(b) Intrinsic muscles of the human hand.

Figure 3: Muscles of the human hand. ByYoung et al. \[[118](#bib.bib118)\], CC BY 4.0.

Muscles interact and work together in a complex way. The force produced by muscles is applied to bones through tendons. Flexors and extensors, for instance, work together to not only control the finger positions but also the force and stiffness of the hand \[[16](#bib.bib16)\].

More than 30 intrinsic and extrinsic muscles move the hand \[[41](#bib.bib41)\] (see Figures [3](#S2.F3 "Figure 3 ‣ 2.1.3 Muscles and Tendons ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?") a and b). They are named according to the type of movement they perform (flexor, extensor, abductor, adductor), the bones they connect to, or the fingers they move. Some have an additional suffix describing their size (longus, brevis) or position (superficialis, profundus). Each Latin name of a muscle is preceded by the term musculus, which we omit for brevity.

##### Wrist (extrinsic muscles, Figure [3(a)](#S2.F3.sf1 "In Figure 3 ‣ 2.1.3 Muscles and Tendons ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?"))

Several muscles work together to flex and extend the wrist joint. Flexor carpi radialis, flexor carpi ulnaris, and palmaris longus flex the wrist joint. Extensor carpi ulnaris, extensor carpi radialis longus, and extensor carpi radialis brevis extend the wrist joint \[[118](#bib.bib118)\]. However, most of these muscles also have another function. All carpi radialis muscles contribute to abduction, and all carpi ulnaris muscles contribute to adduction of the wrist. Furthermore, there are extrinsic finger muscles that contribute to wrist flexion and extension \[[118](#bib.bib118)\].

##### Extrinsic finger muscles, excluding the thumb (Figure [3(a)](#S2.F3.sf1 "In Figure 3 ‣ 2.1.3 Muscles and Tendons ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?"))

The extrinsic flexors and extensors of the fingers act on multiple joints, including the wrist. Most notably are

- •  
Flexor digitorum superficialis (FDS): its four tendons attach to the middle phalanges 2–5 and it flexes the fingers and the wrist.
- •  
Flexor digitorum profundus (FDP): its four tendons attach to the distal phalanges 2–5, passing through the tendons of FDS, and it flexes the fingers and the wrist.
- •  
Extensor digitorum communis (EDC): its four tendons attach to the distal phalanges 2–5 and it extends the fingers and the wrist.

Furthermore, the extrinsic finger muscles extensor indicis and extensor digiti minimi extend all joints of only one finger—index and little finger, respectively—and the wrist.

##### Intrinsic and extrinsic muscles of the thumb (Figure [3(b)](#S2.F3.sf2 "In Figure 3 ‣ 2.1.3 Muscles and Tendons ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?"))

The thumb is an unusual yet essential finger with its large range of motion in the TMC joint and ability to oppose the other fingers. Eight muscles control it. The two degrees of freedom of the TMC joint are controlled by all intrinsic (opponens pollicis, abductor pollicis brevis, flexor pollicis brevis, adductor pollicis) and extrinsic (flexor pollicis longus, extensor pollicis longus, extensor pollicis brevis, abductor pollicis longus) muscles of the thumb. The MCP joint is flexed by flexor pollicis longus and brevis and extended by extensor pollicis longus and brevis. The IP joint is only flexed by flexor pollicis longus and extended by extensor pollicis longus. Abductor pollicis longus also contributes to wrist abduction, and flexor pollicis longus to wrist flexion.

##### Other intrinsic muscles (Figure [3(b)](#S2.F3.sf2 "In Figure 3 ‣ 2.1.3 Muscles and Tendons ‣ 2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?"))

Four dorsal interossei muscles and three palmar interossei muscles perform abduction and adduction of fingers 2–5\. They also assist the lumbricals, which are located between tendons of the FDP at the palm and the back side of the distal phalanges 2–5, in their function. They flex the MCP joints and extend the PIP and DIP joints, allowing for individual flexion of the MCP joints.

There are also specific muscles that have a single function and can be found only in one or two fingers. Abductor digiti minimi: it abducts the little finger so that the abduction of the little finger can be stronger than that of fingers 2–4\. Flexor digiti minimi brevis: flexes the little finger at the MCP joint. Opponens digiti minimi: brings the little finger into opposition, much less than the thumb, though, and also hollows the palm. Palmaris brevis does not seem to be functionally relevant, but provides protection to underlying tissue \[[64](#bib.bib64)\].

#### 2.1.4 Redundancy

Often, multiple muscles work together to perform one movement. For example, seven muscles contribute to controlling the two degrees of freedom of the wrist. This, however, does not mean that muscles are redundant and can be removed, as \[[48](#bib.bib48)\] point out.

#### 2.1.5 Force

\[[113](#bib.bib113)\] report maximal power grip forces of 450 N. \[[111](#bib.bib111)\] observe up to 662 N for the 90th percentile of 25–29 year old men in their dominant hand.

#### 2.1.6 Coupling

It is not possible to completely isolate movements of each degree of freedom. Flexion of one finger causes nearby fingers to move as well (enslaving force phenomenon \[[93](#bib.bib93)\]). The effect increases with the force applied to the main finger. Mechanical coupling between tendons and muscle compartments, multi-digit motor units that co-activate, and overlapping representations in the brain are possible causes. For example, FDP flexes all three finger joints \[[4](#bib.bib4)\].

Another example of coupling is abduction of the index finger, which is facilitated by the dorsal interossei muscle, thereby pulling the thumb closer to the index finger. This movement of the thumb must be compensated for by other muscles, resulting in small movements. However, \[[33](#bib.bib33)\] show that the thumb is the finger that moves most independently. An independently movable and opposable thumb is essential for the prehensile function of the hand.

#### 2.1.7 Variations

The exact dimensions and the range of motion vary from person to person. Even the number of fingers can be different, as some people might have six fingers \[[59](#bib.bib59)\].

#### 2.1.8 Soft cover (muscles and skin)

An often-neglected aspect in robotics is the soft and deformable cover of the human hand, consisting mainly of its intrinsic muscles on the palm side and the skin. By contracting muscles located in the palm or flexing the fingers, the surface can also be deliberately changed.

### 2.2 Sensors of the Human Hand and Perception

#### 2.2.1 Biomechanical aspects of haptic perception

Haptic perception is often linked to the sense of touch, mediated primarily by skin receptors that fall into three categories based on their function: mechanoreceptors for pressure and vibration, thermoceptors for temperature changes, and nociceptors for pain \[[78](#bib.bib78), Chap. 9\]. These receptors allow us to perceive size, shape, texture, and temperature, which are crucial for object manipulation \[[18](#bib.bib18)\].

Proprioception, or the sense of self-movement and body position, is integral to haptic perception. This sense originates from receptors in muscles, joints, and tendons \[[53](#bib.bib53), [17](#bib.bib17)\], playing a key role in perceiving object properties like shape through the alignment of bones and muscle stretching \[[70](#bib.bib70)\]. Proprioceptive receptors in muscles, skin, and joint capsules \[[97](#bib.bib97)\] are crucially connected with motor control \[[100](#bib.bib100)\].

Muscle spindles sense changes in muscle length, while Golgi tendon organs (GTOs) measure muscle-applied force \[[97](#bib.bib97)\], contributing to detailed representations of hand and limb positions. Joint capsule receptors measure extreme positions of the joints to prevent overextension \[[97](#bib.bib97)\]. The proprioceptive signals are highly interconnected with motor control \[[100](#bib.bib100)\] and have a fast conduction velocity of 80–120 m/s \[[92](#bib.bib92)\]. These proprioceptive signals, interacting with tactile feedback, convey information about the state of hand, wrist, and forearm muscles.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig4.png) 

Figure 4: Primary mechanoreceptors in the human skin. Merkel’s cells respond to light touch, Meissner’s corpuscles respond to touch and low-frequency vibrations. Rufinni endings respond to deformations and warmth. Pacinian corpuscles respond to transient pressure and high-frequency vibrations. Krause end bulbs respond to cold. Image from \[[14](#bib.bib14)\] CC BY 4.0.

The classification of mechanoreceptors in the human hand includes four primary types, each with distinct characteristics \[[18](#bib.bib18)\]. Pacinian corpuscles (FA II) are fast-adapting receptors that detect high-frequency vibrations, which are important for tool use, with a typical stimulus frequency range of 40–500+ Hz. Ruffini corpuscles (SA II) adapt slowly and respond to skin stretch, providing feedback on finger position, stable grasp, and tangential forces, with effective stimuli frequencies around 100–500+ Hz. Merkel cells (SA I), also known as slow-adapting, have high spatial acuity (approximately 0.5 mm) and are crucial for texture perception and form detection, responding to low-frequency stimuli between 0.4 and 3 Hz. Meissner’s corpuscles (FA I) are fast-adapting, sensitive to low-frequency vibrations (3–40 Hz), and are involved in motion detection and grip control, with spatial acuity ranging from 3 to 4 mm. All mechanoreceptors exhibit similar conduction velocities of approximately 35–70 m/s, facilitating the rapid relay of tactile information essential for fine motor tasks. They contribute to detecting fingertip forces, vibrations, and tangential loads \[[56](#bib.bib56)\].

Cutaneous nerve fibers on the dorsal hand surface react to skin stretch during joint movements and convey joint angle information \[[57](#bib.bib57)\]. Stimulating the skin on the dorsal surface can induce illusions of movement. However, this effect has only been tested where a single joint was deflected \[[57](#bib.bib57)\].

The brain devotes a significant portion of the somatosensory cortex to the hand, reflecting its behavioral importance. About 20% of the surface in Brodmann’s areas \[[57](#bib.bib57)\] are allocated to hand representations.

#### 2.2.2 Skills enabled by haptic perception

Haptic perception enables humans to explore objects using strategies known as exploratory procedures (EPs) \[[52](#bib.bib52), [53](#bib.bib53)\]. These EPs are categorized based on their focus: the substance of an object (texture, hardness, temperature, weight), structural properties (global shape, volume, weight), and function discovery (movable parts, potential functionality). For instance, the lateral motion EP moves skin over an object’s surface to assess texture, while the pressure EP tests hardness through poking or tapping. Static contact EP assesses temperature briefly through passive touch. Other EPs include unsupported holding for weight inference, enclosing for global shape, contour following for detail, and part motion testing and function testing for understanding movement and function. Figure [5](#S2.F5 "Figure 5 ‣ 2.2.2 Skills enabled by haptic perception ‣ 2.2 Sensors of the Human Hand and Perception ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?") shows examples of the exploratory procedures for the first two categories.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5a.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5b.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5c.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5d.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5e.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig5f.png)

Figure 5: Illustration of six exploratory procedures \[[53](#bib.bib53)\]. From left to right and top to bottom: Contour Following, Pressure, Enclosure, Unsupported Holding, Static Contact, and Lateral Motion. Adapted from \[[71](#bib.bib71)\] CC BY 3.0.

Proprioception, which is the perception of self-movement and body position, plays a crucial role in daily activities and fine motor skills \[[57](#bib.bib57)\]. Lack of proprioception can lead to unstable reach trajectories, impaired postural stability, and poor hand coordination, even when visual feedback is available \[[53](#bib.bib53)\]. Stereognosis, the haptic perception of three-dimensional shapes, requires integrating proprioceptive with cutaneous signals \[[57](#bib.bib57)\]. Proprioceptive signals describe hand conformation during grasp, while tactile signals deliver contact location and geometric features such as edges and corners at each contact point \[[57](#bib.bib57)\]. This integration ensures effective object perception and showcases how multimodal signals encode object identity even before contact occurs \[[57](#bib.bib57)\].

#### 2.2.3 Role in Grasping

Tactile information is crucial for reaching and grasping, with cutaneous receptors playing a vital role in controlling prehensile force during object manipulation \[[18](#bib.bib18)\]. These receptors help determine the shear or load force, enabling optimal adjustment of grip force \[[18](#bib.bib18)\]. Tactile feedback provides information about the system’s state; without it, internal models that guide anticipatory control mechanisms become outdated, complicating tasks like grasping \[[18](#bib.bib18)\]. Specific tactile afferent responses characterize the distinct phases of a grasping action—such as reaching, loading, lifting, and holding—marking transitions between these phases and centering the planning and control of manipulation in the brain on mechanical events \[[18](#bib.bib18)\].

Effective grasping demands fine control over finger muscle strength and precise timing throughout various phases of grasp. A lack of tactile sensing can prolong the duration of the finger opening phase, impairing grasp control and coordination \[[18](#bib.bib18)\]. Tactile cues at the beginning and end of movements enable the optimization of grasp temporal parameters, facilitating an understanding the timing of sequential actions, such as playing an instrument or executing synchronized movements \[[18](#bib.bib18)\].

While tactile senses are pivotal, the human sensory system is inherently multimodal, integrating touch, vision, and auditory feedback to construct a comprehensive internal representation known as the “body schema” \[[18](#bib.bib18)\]. This integration increases the reliability of sensory estimates and enhances robustness \[[18](#bib.bib18)\]. In grasping, a precise measure of contact forces is essential for force control and maintaining stable grasps \[[18](#bib.bib18)\].

In addition to understanding the magnitude of forces, the direction is critical for dexterous manipulation, as it regulates the balance between normal and tangential forces to ensure grasp stability, known as the “friction cone” \[[18](#bib.bib18)\]. Shear forces provide crucial insights into shape, surface texture, and slip, forming a significant part of the tactile information required for interacting with objects and discerning material properties such as hardness and temperature \[[18](#bib.bib18)\].

### 2.3 Theories of Human Motor Control and Learning

We can place human motor functions on a spectrum from involuntary to voluntary. The most involuntary motor functions are reflexes, which have a direct neural connection between stimulus and response. Additionally, more complex, automated movements, such as locomotion patterns, are involuntary. Voluntary movements include consciously controlled movements such as grasping, writing, and speaking. In the hierarchy of movements, speaking might be a voluntary act, but forming individual vowels is a highly automated, less voluntary process. Several theories explain various aspects of human movements, control, and motor learning.

#### 2.3.1 Central Nervous System (CNS)

We summarize the role of the CNS for motor control based on \[[10](#bib.bib10)\].

##### Motor cortex

The motor cortex produces higher motor functions and contains cortical columns that represent individual movements, involving the coordination of multiple muscles. The primary motor cortex executes voluntary movements, controls muscles directly, and efferent nerve fibers connect it to, e.g., the basal ganglia, secondary motor areas, thalamus, cerebellum, and the spinal cord. Some pyramidal cells of the primary motor cortex connect monosynaptically to the muscles of the hand to perform a precision grasp, which humans develop during the first year of their life. The premotor cortex initiates and plans movements that are sensomotorically triggered and guided. The supplementary motor area is responsible for planning self-initiated movements and coordinating voluntary movement with other actions.

##### Cerebellum

The cerebellum coordinates, optimizes, and corrects movements. It compares desired effects with sensor feedback and learns from errors. Specifically, the spinocerebellum moves distal muscles (e.g., for grasping) and receives afferences from the spinal cord for fast control of trajectories based on comparison between desired movements with anticipated sensor measurements and actual measurements. This process happens mainly for new, non-repetitive movements. The pontocerebellum plans and controls temporally or spatially complex movements, e.g., coordinates the simultaneous movement of fingers. It stores motor programs, which are complex, automated movements that have been learned and do not use sensor feedback. The pontocerebellum is primarily involved in complex and fast movements, e.g., playing the piano.

##### Basal ganglia

The basal ganglia support flexible control of higher motor functions. They execute or suppress learned movements based on context (situation-movement associations), select from several possible movements, are responsible for temporal coordination, and learn from rewards.

#### 2.3.2 Motor Program Theory

Motor program theory explains learning, representation, and execution of fast, open-loop motor skills that are realized in the pontocerebellum. It is based on the observations that reaction time increases with complexity of movements \[[76](#bib.bib76)\], animals that are deprived of sensory information using a surgical process of deafferentation still produce effective movements \[[76](#bib.bib76)\], and muscular activity patterns during the first ca. 100 ms of limb movement remain the same even when a person’s limb is unexpectedly prevented from moving \[[109](#bib.bib109)\]. \[[86](#bib.bib86), [87](#bib.bib87)\] proposed generalized motor programs (GMPs) and the schema theory for learning fast, open-loop motor skills. GMPs are representations of complex, coordinated, and rapid movements that are learned and allow modification along several dimensions, such as movement time, movement amplitude, and the effector system used to produce the action, thereby preserving the temporal pattern of the movement. Schema theory extends GMPs. It suggests that tuples of situation / context parameters, GMP parameters, extrinsic feedback (result of movement), and internal feedback (sensor information) are used to form schemas. When encountering a situation, an appropriate GMP and parameterization are selected to achieve the desired result.

#### 2.3.3 Dynamical Systems Theory

Another theory is needed to explain closed-loop, sensorimotor control. An interesting observation is that humans have many degrees of freedom, e.g., in their hands and arms, that need to be coordinated, many more degrees of freedom than are necessary to solve specific tasks. \[[6](#bib.bib6)\] found that humans reliably reach high-level goals despite high variability in their movements. A related phenomenon is the so-called uncontrolled manifold \[[88](#bib.bib88)\], which states that several degrees of freedom are actively controlled and stable. In contrast, others are not controlled and show high variability. Dynamical systems theories \[[94](#bib.bib94)\] explain these observations through concepts such as muscle synergies and coordinative structures that result in attractor states or dynamic stability with many redundant degrees of freedom \[[89](#bib.bib89), [28](#bib.bib28)\]. The concept of synergies has been applied to hand control by \[[58](#bib.bib58)\], who demonstrate that reach-to-grasp motions can be produced with a base posture with refinements of finger positions. The first three dimensions of a singular value decomposition account for 99.5% of the variance of all observed grasps. Hence, it is assumed that actively controlled degrees of freedom are considerably lower than the actual number of degrees of freedom of the hand. \[[84](#bib.bib84)\] apply the concept to forces. Synergies describe the outcome, but their origin needs an additional explanation.

#### 2.3.4 Stochastic Optimal Feedback Control

\[[102](#bib.bib102), [101](#bib.bib101)\] propose stochastic optimal feedback control to combine performance guarantees inherent in optimization models with behavioral richness emerging from dynamical systems. \[[102](#bib.bib102)\] argue that planning and execution are not separated. This framework explains task-constrained variability, goal-directed corrections, motor synergies, and controlled parameters, simplifying rules and discrete coordination modes into a unifying theory of sensorimotor skills.

#### 2.3.5 Bayesian Decision Theory and Predictive Motor Control

Humans exhibit behavior similar to Bayesian processes in motor control, perception integration, and cue combination \[[46](#bib.bib46)\], which enables them to handle noise in the environment, perception, and their movements \[[23](#bib.bib23)\]. Combining prior knowledge with sensory feedback provides more certainty than sensory feedback alone \[[26](#bib.bib26)\]. Bayesian decision theory extends this to motor control. It is a probabilistic framework that models action selection as a way to maximize the expected utility of an outcome, where the utility quantifies the overall desirability of the outcome of a movement decision. Humans constantly predict expected sensor measurements \[[115](#bib.bib115), [114](#bib.bib114), [44](#bib.bib44)\] and compare them to actual measurements, e.g., in the spinocerebellum. This theory is compatible with optimal feedback control \[[102](#bib.bib102), [101](#bib.bib101)\].

#### 2.3.6 Sensorimotor Learning

\[[116](#bib.bib116)\] distinguish various processes of motor learning: (1) error-based learning that uses a gradient with respect to each component of the motor command to adapt motor commands (e.g., grip force) quickly, (2) reinforcement learning for complex sequences of actions that need to take place to achieve a goal and the outcome is far removed from the action, and (3) use-dependent learning that changes the behavior, even if no outcome information is available. In addition, humans can learn high-level information about which movements to make in sequence and how to compensate for perturbations from observing others.

### 2.4 Summary: Defining Characteristics of the Human Hand

#### 2.4.1 Biomechanics

The human hand has five fingers, an opposable thumb, a high number of about 24 degrees of freedom, including abduction/adduction and three flexion/extension joints per finger, of which most of them are almost individually controllable, an extensive active and even larger passive range of motion, a soft and deformable surface, particularly at the large surface of the flexible palm, and the ability to produce high grip forces. Individual control of each degree of freedom is not perfect for several reasons: muscles that move multiple joints, coupling and friction between tendons, co-activation of motor units, and representation in the brain. For instance, strong forearm muscles flex multiple fingers and joints per finger simultaneously to generate a firm power grasp. Flexion of just one joint requires coordination of multiple muscles.

#### 2.4.2 Perception

The human hand robustly integrates tactile and proprioceptive signals across skin, muscle, and joint receptors. This integration enables the perception of detailed object properties and nuanced positional feedback, forming a sophisticated multimodal sensory system. Such complexity in perception is a key inspiration for developing advanced robotic hands that mimic human dexterity and precision.

#### 2.4.3 Control and Learning

Different mechanisms seem to be responsible for controlling and acquiring fast, complex, repetitive skills without sensor input, versus new or perception-based skills that require constant control. Often, human control aims at optimality and does not explicitly encode which limb or muscle is used. Humans integrate sensor data from various high-dimensional sources (visual, tactile, kinesthetic) and easily coordinate many degrees of freedom. They can handle sensor and actuator noise in a Bayesian-like way and anticipate sensory feedback. However, the most important feature of human control is its adaptability through learning and continuous improvement with additional experience.

## 3 Robotic Hands

Given the open question of whether anthropomorphic hands are genuinely needed, we take a closer look at existing robotic hands and sensors in both research and commercial contexts. Broadly, these can be divided into two categories: robotic hands developed by companies and research institutions for versatile manipulation tasks, and prosthetic hands designed to replace lost or missing human limbs. While the former focuses on enabling machines to interact flexibly with their environment, the latter are tailored to specific user needs and medical contexts.

In this section, we provide a detailed analysis of the most widely known and used robotic hands across industrial, research, and prosthetic domains. We focus on their design choices, sensory capabilities, and key features. A more comprehensive overview is provided in the supplementary material.

### 3.1 Mechanics

Robotic hands are designed in various ways depending on their intended use. \[[16](#bib.bib16)\] suggest considering six aspects when designing a robotic hand: (1) hand kinematics, (2) actuation principle, (3) actuation transmission, (4) sensors, (5) materials, and (6) manufacturing method.

The required DoFs and the number of actuators determine the hand’s kinematics \[[16](#bib.bib16)\]. The mechanical fingers/grippers are mainly composed of different joints connected in a serial manner, allowing them to perform a specific task. In order to be able to control nn DoFs, we need m\=n+1m=n+1 independent actuation tendons \[[16](#bib.bib16)\]. Such kinematic architecture is used in the BarrettHand222<https://advanced.barrett.com/barretthand>. Nevertheless, hands with actuation tendons that exceed n+1n+1 are more versatile and dexterous. These kinematic architectures are called redundant and are used, for example, in The Shadow Dexterous Hand333[https://www.shadowrobot.com](https://www.shadowrobot.com/).

Regardless of the advantages of using redundant transmission, it is also possible to design hands with underactuation (m<nm<n) and coupled transmission. Such a design is inspired by the human hand, as shown in Section [2.1](#S2.SS1 "2.1 Biomechanics of the Human Hand ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?").

\[[16](#bib.bib16)\] provides six possible kinematic architectures in robotic hands, depicted in Figure [6](#S3.F6 "Figure 6 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?").

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x2.png) 

Figure 6: Representation of possible robotic hand kinematic architectures, adapted from \[[16](#bib.bib16)\]. MM denotes the number of actuated tendons (red circles), and NN the number of bidirectional DoFs (black circles). Diagrams show: (a) M\=NM=N coupled joints; (b) M<NM<N underactuated transmission; (c) M\=NM=N fully actuated open chain; (d) M\=NM=N fully actuated closed chain; (e) M\=N+1M=N+1 fully controllable; (f) M\=2​NM=2N agonist/antagonist transmission \[[16](#bib.bib16)\]. Continuous lines indicate tendons, dashed lines joints, and zigzag lines springs.

The Shadow Dexterous Hand is one of the most advanced robotic hands and is produced by Shadow Robot. It has five fingers and 24 DoFs, of which 20 are controllable. In addition, similar to the human hand, it is possible to perform opposition and reposition of the thumb, flexion, extension, adduction, and abduction of all fingers. Such movements enable a dexterous hand that can perform various complex manipulation tasks.

Figure [7(c)](#S3.F7.sf3 "In Figure 7 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?") represents the kinematic architecture of the Shadow Dexterous Hand using the kinematic notations derived from \[[110](#bib.bib110)\] and depicted in Figure [7(a)](#S3.F7.sf1 "In Figure 7 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?").

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x3.png) 

(a) Legend for kinematic diagrams.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x4.png) 

(b) BarrettHand.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x5.png) 

(c) Shadow Dexterous Hand.

Figure 7: Kinematic diagrams. Notation based on \[[110](#bib.bib110)\]. 

A less complex robotic hand is the BarrettHand. It has three fingers and eight DoFs, although only four of these are independently actuated using four motors. All fingers support flexion and extension movements. Opposition and reposition are possible with two fingers. The kinematic architecture of the BarettHand is depicted in Figure [7(b)](#S3.F7.sf2 "In Figure 7 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?").

Apart from the chosen kinematic architecture, the transmission actuator mechanism and kind do impact the performance of the robotic hand. For instance, actuators used in the artificial hand can be electrical (e.g., DC motors), pneumatic, or hydraulic. Natural muscles have a power density (ρ\\rho) of approximately 500​W/K​g500W/Kg. Such power density can be achieved by hydraulic or pneumatic actuators (respectively, 2000​W/K​g2000W/Kg and 400​W/K​g400W/Kg) \[[32](#bib.bib32)\]. Such solutions are already used in artificial robotic hands (e.g., GRIPKIT Industrial (P PRO)444<https://weiss-robotics.com/gripkit-for-cobots/>, EHA hand \[[45](#bib.bib45)\]). However, such solutions are usually bulky or hard to maintain. DC motors (electrical actuators), on the other hand, can reach a power density ρ\=100​W/K​g\\rho=100W/Kg \[[32](#bib.bib32)\]. While these actuation mechanisms may have a lower power-to-weight ratio compared to others, they remain popular actuators thanks to their compact size and cost-effective maintenance \[[16](#bib.bib16)\].

In order to accurately control joints, transmission is crucial. Such systems enable converting the power provided by the actuators to a specific hand/finger movement. An ideal transmission system would have low inertia, friction and backlash, and would be overall compact and small (i.e., in terms of size and weight). Several transmission types can be deployed: including tendons, gear trains, belts, linkages or flexible shafts \[[16](#bib.bib16)\]. In the human hand, we found tendons that connect muscles to bones \[[98](#bib.bib98)\]. Such tendons run in a sheath. A similar system is commonly found in artificial robotic hands, as such a design allows for reduced friction and remote control of the fingers (e.g., Shadow dexterous hand). For further transmission comparison, we refer to the work of \[[16](#bib.bib16)\].

We reviewed various robotic hands used in industry, research, and also as prosthetic hands. To provide readers and practitioners with a straightforward overview of the commonly used hand, we first categorize these into two groups: robotic hands and prosthetic hands. This splitting is based on the primary application for which the manufacturer/researcher intended the hand to be designed.

We focus on six different features: DoF, number of actuators, number of fingers, possibility of flexion (and extension), adduction (and abduction), and opposition (and reposition). Specifically, DoF and the number of actuators influence the hand’s dexterity and versatility, while the number of fingers and their movement capabilities affect its grasping and manipulation abilities. For a detailed description of each robotic hand, please refer to the supplementary material. The characteristics of robotic and prosthetic hands are visualized in Figure [8](#S3.F8 "Figure 8 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?").

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x6.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x7.png)

(a) Radar diagram of some selected robotic hands. The same color is used for hands developed by the same manufacturer.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x8.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x9.png)

(b) Radar diagram of some selected prosthetic hands.

Figure 8: Radar diagrams of prosthetic and robotic hands. Figure [16](#A1.F16 "Figure 16 ‣ Appendix A Radar Diagram of Skills ‣ Do Robots Really Need Anthropomorphic Hands?") provides a similar diagram for manipulation skills.

### 3.2 Perception

To perform dexterous manipulation, a robot must understand what the object being manipulated is and what type of operation is required, i.e., task requirements \[[117](#bib.bib117)\].

Tactile sensors are primarily designed to mimic mechanoreceptors, particularly for detecting mechanical pressure. The main objectives of tactile sensors are to determine the location, shape, and intensity of contacts. These properties are determined by measuring the instantaneous pressure or force applied to the sensor’s surface on multiple contact points. Also, the contact’s late effects, i.e., body-borne vibrations, may carry relevant information. Body-borne vibrations are not as commonly measured or exploited as part of haptic sensing; however, there are some examples and it is becoming an active area of research \[e.g., [37](#bib.bib37), [9](#bib.bib9), [107](#bib.bib107)\], including sensors that are inspired by the hair follicle receptors or ciliary structure \[[3](#bib.bib3), [39](#bib.bib39)\] and that have been proven effective in obtaining information about the texture of objects \[[80](#bib.bib80), [79](#bib.bib79)\].

Thermoceptors, although an integral part of human haptic perception, are typically not classified as tactile sensors within robotic applications. However, they are sometimes included because they might help compensate for thermal effects \[[103](#bib.bib103)\], thus helping to obtain a more robust electronic signal related to pressure or vibrations, or because they might help to classify the material of the object in contact \[[108](#bib.bib108)\]. In contrast, nociceptors have not yet been developed as part of haptic or tactile sensing per se, but can be and have been implemented in software based on the limitations of robots \[[69](#bib.bib69), [68](#bib.bib68)\].

Overall, artificial tactile sensors are much less established than artificial visual receptors, e.g., RGB(-D) cameras, and event-based cameras. Technologies for tactile sensing have been developed since the early 1970s and have undergone significant improvements in the past decade \[[18](#bib.bib18), [17](#bib.bib17), [42](#bib.bib42)\]. However, the field remains young, and there are no widely accepted solutions. Several transduction methods have been explored, including capacitive \[[51](#bib.bib51)\], piezoelectric \[[90](#bib.bib90)\], piezoresistive \[[38](#bib.bib38)\], optical \[[112](#bib.bib112), [47](#bib.bib47)\], fiber optics \[[77](#bib.bib77)\], and magnetic \[[34](#bib.bib34)\]. Table [1](#S3.T1 "Table 1 ‣ 3.2 Perception ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?") summarizes the advantages and disadvantages of the different transduction principles for detecting mechanical pressure. For additional information, please refer to \[[13](#bib.bib13)\].

Table 1: Transduction mechanisms for detecting mechanical pressure. Tactile sensor design is benefiting from advancements in nanomaterial and nanocomposite fabrication technology. This table is based on \[[13](#bib.bib13)\].

Current prosthetic hands such as the Bebionic and i-Limb hands, have five individually actuated digits, yet only one grasp function can be controlled at a time. Most people commonly use their natural hands to manipulate, grasp, or transport different objects simultaneously. For example, sending commands to multiple fingers while typing on a keyboard, holding a remote control while pressing its buttons, opening a door while holding a bag, or braiding a child’s hair. Such functionalities remain elusive for prosthetic hand users, despite artificial hands being mechanically capable of such feats. Enabling refined, dexterous control is a complex problem. It continues to be an active area of research because it necessitates not only the interpretation of human grasp control intentions, but also complementary haptic feedback of tactile sensations \[[2](#bib.bib2)\].

More research on the impact that multiple channels of haptic feedback have on the ability to multitask with an artificial hand will be an important question to answer so that limb-absent people can exploit the full dexterity of prosthetic limbs \[[2](#bib.bib2)\].

#### 3.2.1 Commercial Sensors

Although there are some commercial solutions, the costs are still relatively high, and the performance level is not always satisfactory. In the rest of this section, we present some of the commercial solutions for tactile sensing. Although we are aware of other commercial sensors such as the WTS-FT by Weiss Robotics GmbH & Co. KG. and BioTac® by SynTouch®, here we only present those that are undoubtedly still being produced and commercialized at the time of writing.

Seed Robotics’ FTS Tactile pressure sensors (see Figure [9](#S3.F9 "Figure 9 ‣ 3.2.1 Commercial Sensors ‣ 3.2 Perception ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?")) are low-cost sensors with high-resolution contact force measurement capabilities (1mN to 30N range). The sensor compensates for temperature and is immune to magnetic interference.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig9a.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig9b.png)

Figure 9: Left: the SINGLEX stand-alone tactile pressure sensor version. Right: FTS tactile pressure sensor mounted on a robot finger. Images used with permission from Seed Robotics (<https://www.seedrobotics.com/>).

The uSkin sensor \[[104](#bib.bib104)\] by Xela Robotics is a magnetic tactile sensor composed of small magnets embedded in a thin layer of flexible rubber and placed above a matrix of magnetic Hall-effect sensor chips. Upon contact, the magnets are displaced, and the magnetic field sensed by the Hall-effect chips changes; the contact forces can be estimated from these variations in the magnetic field. The uSkin sensor can measure the full 3D force vector (i.e., both normal and shear contact forces) at each tactel, with a good spatial resolution (about 1.6 tactels for square cm), high sensitivity (minimum detectable force of 1gf), and high frequency (\>100\>100Hz, depending on the configuration). Different versions of the sensor are available to cover both flat and multi-curved surfaces, see Figure [10](#S3.F10 "Figure 10 ‣ 3.2.1 Commercial Sensors ‣ 3.2 Perception ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?") for an example.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig10a.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig10b.png)

Figure 10: Left: a flat version inspired by \[[105](#bib.bib105)\]. Right: a multi-curved version inspired by \[[106](#bib.bib106)\]. Images with permission from Xela Robotics (<https://xelarobotics.com/>).

The GelSight Mini \[[119](#bib.bib119)\] and DIGIT \[[49](#bib.bib49)\] tactile sensors by GelSight are optical tactile sensors that utilize a piece of elastomeric gel with a reflective membrane coating on top, enabling them to capture fine geometrical textures as deformations in the gel. A series of LEDs with RGB colour illuminates the gel, allowing a camera to record the deformation.

Finally, Contactile offers both a stand-alone sensor and tactile sensor arrays, called PapillArray sensors, as shown in Figure [11](#S3.F11 "Figure 11 ‣ 3.2.1 Commercial Sensors ‣ 3.2 Perception ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?"). These optical sensors consist of infrared LEDs, a diffuser, and four photodiodes encapsulated in a soft silicone membrane. The photodiodes are used to measure the light intensity patterns, which are then used to infer the displacement and force applied to the membrane. This strategy enables the measurement of 3D deflections, 3D forces, and 3D vibrations, as well as the inference of emergent properties such as torque, incipient slip, and friction.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig11a.jpg)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/Fig11b.jpg)

Figure 11: Left: Single 3D force tactile sensor. Right: A slim tactile sensor array (PapillArray Sensor) available in different configurations. Images from Contactile (<https://contactile.com/>), licensed under CC BY-NC-ND 4.0.

The need for such technologies is driving research forward in both the development of new sensing technologies and applications such as robotic grasping, smart prostheses, and surgical robots. In particular, enhancements are still needed in the mechanical robustness, sensitivity, and reliability of the measurements, as well as the ease of electromechanical integration and replacement, to deploy sensors in practical applications. Of particular interest are solutions that: are flexible \[[51](#bib.bib51), [91](#bib.bib91)\], stretchable \[[11](#bib.bib11)\] and can cover sizeable \[[19](#bib.bib19)\] and curved \[[106](#bib.bib106)\] surfaces (possibly with a small number of electrical connections \[[37](#bib.bib37)\]), can detect multiple contacts at the same time \[[31](#bib.bib31)\], can detect both normal and shear forces \[[105](#bib.bib105)\], are affordable and can be easily manufactured \[[74](#bib.bib74)\]. For more information on experimental tactile sensing technologies, see \[[13](#bib.bib13)\], and for a specialized review of printable, flexible, and stretchable tactile sensors, see \[[91](#bib.bib91)\].

#### 3.2.2 Tactile Servoing

The dexterous robotic hand can achieve more accurate adjustments through the combination of real-time tactile feedback and the control system. The sense of touch is no longer simply “telling” the robot about contact information and object information. Robot hands use tactile information to make judgments about fingers and control the object’s state to reach the target state. In control-level perception, related research topics include tactile servoing, slip detection, and grasp quality measures \[[117](#bib.bib117)\].

##### Tactile servoing

In the process of dexterous manipulation, the tactile servo can be assigned in the control architecture, where the motor is driven by tactile feedback. Meanwhile, tactile servoing also gives the robotic hand a new direction for exploring new environments more safely \[[117](#bib.bib117)\].

##### Slip detection

Dexterous manipulation with a multi-fingered robotic hand is a challenging task due to the existence of uncertainties arising from sensor noise, slippage, or external disturbances. External disturbances caused by environmental changes may cause a planned-to-be stable grasp to become unstable. Humans can react quickly to instabilities through tactile sensing. The ability to detect slips in tactile perception is critically essential for further dexterous manipulations \[[117](#bib.bib117)\].

##### Grasp quality measure

The correct grasp of objects is critically important for dexterous manipulation. Planning a good grasp involves determining grasping points on the object surface and selecting suitable hand configurations. Given an object and a hand, the key step in grasping planning is to measure the grasp quality \[[117](#bib.bib117)\].

### 3.3 Robot Control

Numerous approaches have been used to generate motor skills for robots. A list that is most likely not complete: motion and grasp planning, optimal control, model-predictive control, reinforcement learning (model-free / model-based), inverse reinforcement learning, offline reinforcement learning, imitation learning (e.g., through teleoperation, kinesthetic teaching, and retargeting), and evolutionary algorithms. Robotics research and neuroscience have a significant overlap as demonstrated, for example, by \[[94](#bib.bib94)\] or \[[101](#bib.bib101)\]. Theories that explain human behavior often yield practically useful concepts for movement generation in robotics.

#### 3.3.1 Planning

Motion planning \[[43](#bib.bib43)\] and grasp planning, utilizing tools such as GraspIt! \[[60](#bib.bib60)\] and grasp quality measures \[[81](#bib.bib81)\], are traditional approaches for generating robot motion. However, they often assume a noise-free, controlled environment, and it is challenging to define arbitrary manipulation tasks beyond grasping or pick-and-place.

#### 3.3.2 Dynamical Movement Primitives

An approach to robot control that combines aspects of generalized motor programs and schema theory on the one hand and dynamical systems theory on the other is dynamical movement primitives (DMPs, \[[85](#bib.bib85)\]). DMPs define stable dynamical systems to generate motor commands, and can be learned from demonstration and through reinforcement learning. Similar to the concept of schema theory, regression techniques can be used to parameterize DMPs based on context or task parameters.

#### 3.3.3 Stochastic Optimal Feedback Control, Optimal Control, Model-Predictive Control, and Reinforcement Learning

In contrast to neuroscience, the field of robot control distinguishes optimal control and model-predictive control from model-free and model-based reinforcement learning (RL). In optimal control and model-predictive control, the models are explicitly defined, while they are learned or not explicit in RL. As a result, developed algorithms often differ.

Optimal control has been implemented in robotic systems to generate movements in various forms. \[[65](#bib.bib65)\] generate complex manipulation actions for various hands through optimization with an a priori defined model of the system and environment. However, a similar approach can be used continuously online with a high frequency, which is known as model-predictive control, to generate complex movements as shown by \[[99](#bib.bib99)\] in the context of locomotion. This approach is robust to model errors.

In model-based RL, dynamics models and reward models are learned from experience. \[[67](#bib.bib67)\] demonstrate how to use a model for online optimization of actions in various manipulation tasks, e.g., in-hand manipulation. Model-free RL solves the problem without explicitly learning the dynamics model. The most successful approaches for continuous control \[e.g., [73](#bib.bib73), [120](#bib.bib120)\] are based on the actor-critic framework, which directly learns a policy that maps observations to actions, eliminating the need for online optimization. RL can solve complex tasks, such as playing piano \[[120](#bib.bib120)\].

Although these approaches are promising and attempt to mimic human motor control, in practice, they often fail to integrate complex sensory data. They could, but even though camera images are sometimes used directly as input, they are often avoided \[e.g., [67](#bib.bib67)\] or enriched with additional position information \[e.g., [73](#bib.bib73)\]. In comparison to human motor control, we often overlook the integration of additional sensors, such as tactile sensors. In addition, learning and adaptation of behavior typically do not occur online, even with machine learning approaches, after the initial training stage is completed.

#### 3.3.4 Vision-Language-Action Models

Motivated by the success of large pretrained vision and language models, vision-language-action models (e.g., RT-2 \[[122](#bib.bib122)\]) trained on teleoperation data are a novel imitation learning approach for visuo-motor skills. Although this learning paradigm is still in its early stage of research, it appears promising, as integrating other sensor modalities seems possible.

### 3.4 Summary

#### 3.4.1 Mechanics

From a mechanical perspective, the most advanced robotic hands, such as the Shadow Dexterous Hand, can replicate the number of fingers and degrees of freedom found in a human hand. However, they lack the flexibility, deformability, and the passive range of motion inherent in human joints. Achieving high dexterity often comes at the expense of reduced force production. This trade-off between dexterity and force limits the overall performance of robotic hands, highlighting the need for further research in areas such as material science, mechanical design, and control systems.

#### 3.4.2 Sensors

From a perceptual perspective, human hands have a vast array of sensors, including mechanoreceptors, thermoreceptors, and nociceptors, which provide detailed information about touch, texture, temperature, and potential for damage (Section [2.2](#S2.SS2 "2.2 Sensors of the Human Hand and Perception ‣ 2 The Human Hand ‣ Do Robots Really Need Anthropomorphic Hands?")). This sensory input is essential to perform a wide range of object manipulations, allowing humans to adjust their grip forces and hand or finger positions in real time. In contrast, robotic hands rely on a limited number of tactile or force sensors, which are often bulky compared to the size of the robotic fingers and provide only partial information about the environment. Additionally, the data from these sensors requires post-processing to be interpreted and used effectively in manipulation tasks. These limitations suggest the need for further development in both the design and signal processing aspects of robotic perception sensors.

#### 3.4.3 Control and Learning

We have seen rapid progress in robot control recently, with groundbreaking works on control of complex hands \[e.g., [73](#bib.bib73)\]. However, the integration of complex sensory feedback and complex hands remains an open challenge, and online learning and adaptation are not the primary focus. Although the control approaches are similar to those used by humans, they do not reach human dexterity.

## 4 Systematic Review of Robotic Hands and their Skill Repertoire

We performed a systematic literature review to connect hands with the skills they can perform. We use a simplified version of the PRISMA approach \[[61](#bib.bib61)\] as we did not aggregate the results of empirical studies with reported statistical results, but merely collect information on demonstrated robot skills.

### 4.1 Methods

#### 4.1.1 Search Strategy

We extracted information about which hand was used to perform which skills. For this purpose, on May 7t​h7^{th} 2025, we searched in the following databases:

- •  
Google Scholar with the search term (hand or gripper) and (manipulation or grasping or grip or skill). Google Scholar is one of the largest scientific databases indexing scientific articles, preprints, and university websites.
- •  
IEEE Xplore with the search term (hand or gripper) and (manipulation or grasping or grip or skill). IEEE is one of the main publishers of robotic research, also indexing articles from a few other publishers.

We extracted the title, number of citations, year of publication, source (e.g., journal, conference), publisher, text snippet, and URL from Google Scholar. We extracted the title, number of citations, year of publication, source, abstract, URL, and keywords from IEEE Xplore. These records were filtered and selected in the following step.

#### 4.1.2 Selection

##### Automatic filtering

We filtered the results from Google Scholar and IEEE Xplore using the following criteria: publication dates must be between 2019 and 2025, the article must have at least one citation, be at least four pages long, and be written in the English language. All IEEE papers were removed from the initial set retrieved using Google Scholar to eliminate duplicates. All non-peer-reviewed articles published on arXiv were removed from our list. Finally, we filtered IEEE papers based on the keyword terms to ensure they contain one of these terms: (hand or gripper) and (manipulation or grasping or grip or skill).

##### Manual screening of records

In a manual screening step, we excluded papers not related to robotic or prosthetic hands or grippers based on the title, abstract, or text snippet. These often involve measurements of hand grip strength in humans or other topics in the medical field.

##### Assessment of full-text articles

After automatic filtering and manual prescreening, we kept papers demonstrating skills with multi-fingered hands (≥2\\geq 2 fingers) beyond simple pinch grasps. We exclude papers with the following criteria.

- •  
Virtual reality / augmented reality
- •  
Gripper / hand design / development without demonstration of skills beyond flexion/extension of fingers
- •  
Development of sensors or perception approaches without demonstration of skills beyond flexion/extension of fingers
- •  
Non-anthropomorphic gripper designs, such as soft fingers or suction mechanisms

#### 4.1.3 Data collection process

For each article, we extract the hand and its features, sensor setup, and skill categories that were presented or are trivially possible to implement with the hand shown in the article.

##### Hand features

The features that we use to characterize the hand and sensor setup are: number of fingers, degrees of freedom, number of actuators, mechanism features (such as use of the palm, switching between thumb reposition and opposition, switching between abduction and adduction, switching between flexion and extension), sensor features (tactile / kinesthetic / visual feedback used or not). We selected these features because they are defining characteristics of the human hand and manipulation capabilities. At the same time, they are achievable by state-of-the-art robotic hands.

##### Skill repertoire

We examined the papers and extracted any skills or movements that the authors claim to have generated for a real or simulated robotic hand. These manipulation skills were then categorized according to the taxonomy of manipulation tasks by \[[21](#bib.bib21)\]. The taxonomy encompasses both prehensile skills, such as grasping and in-hand manipulation, and non-prehensile skills, including pushing and gestures. It is designed to be independent of the hand morphology. Furthermore, for in-hand manipulation categories (14 and 15: Contact / Motion / Within Hand / (No) Motion at Contact), we extract the degrees of freedom of an object that are manipulated.

#### 4.1.4 Risk of bias in individual studies

We see the risk of underreported skill repertoires for the robotic hands. Not all hands fully exhaust their skill repertoire in the respective publication. Even though we aggregate results from various publications using the same hand, we can not be sure that the hand would not be able to perform an in-hand manipulation skill with more DoF or another category of skills not seen in the publication. Thus, it is likely that some skills that a hand would be able to perform are not investigated in the respective publication. For instance, the users of prosthetic hands may be able to perform a large variety of skills in their daily lives that are not reported in any publication. As a result, we analyze extreme cases, e.g., the minimum complexity of a hand required to implement a specific skill.

#### 4.1.5 Summary measures and synthesis of results

If a hand is used in multiple papers, we aggregated the results by accumulating all sensor features and performed skills. We summarized the results in the following charts.

##### Histogram of hand and sensor features

To get an overview of the distribution of hand and sensor features of the presented hands, we will present histograms of these features.

##### Percentage of achieved skills by hands

We use bar charts to show the percentage of hands with specific features that demonstrate the ability to perform each skill category. Although in theory, each skill category should be covered by each hand, this analysis gives us an impression of how thoroughly the skill repertoire has been examined.

##### Correlation analysis

We compute Pearson’s product-moment correlation coefficient rr between the mechanism features and the DoF of the two in-hand manipulation categories. With α\=0.05\\alpha=0.05, we test statistical significance using two-sided t-test for td​f\=r⋅N−21−r2t\_{df}=\\frac{r\\cdot\\sqrt{N-2}}{\\sqrt{1-r^{2}}}, d​f\=N−2df=N-2 (NN: number of samples).

##### Analysis of extreme cases

We plot the distribution of hand features that define the hand’s complexity versus skill complexity to identify extreme cases. More specifically, we look for simple hands that can perform complex skills.

### 4.2 Results

#### 4.2.1 Selection

Figure [12](#S4.F12 "Figure 12 ‣ 4.2.1 Selection ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?") summarizes the selection process. We include 125 papers in the summary. See supplementary material for an overview of included articles, <https://figshare.com/s/f4fdd9aca1c134f010dd>.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x10.png) 

Figure 12: Summary of selection process.

#### 4.2.2 Synthesis of results

##### Histogram of hand and sensor features

Figure [13](#S4.F13 "Figure 13 ‣ Histogram of hand and sensor features ‣ 4.2.2 Synthesis of results ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?") shows a summary of the hand characteristics for all hands in the analyzed papers.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x11.png) 

Figure 13: Histograms (max. of 10 bins) of the characteristics of the hands that we analyzed in this systematic review.

##### Percentage of achieved skills by hands

Figure [14](#S4.F14 "Figure 14 ‣ Percentage of achieved skills by hands ‣ 4.2.2 Synthesis of results ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?") shows the percentage of hands that can perform a skill from the respective skill category, ordered by features of the hands. We only show the result for four skill categories (5 (e.g., pushing a coin), 8 (e.g., rolling a ball on a table), 11 (e.g., turning a doorknob), 13 (e.g., writing) of Dollar’s \[[21](#bib.bib21)\] taxonomy due to space constraints. These skill categories represent a wide range of different skills; for example, two of them are prehensile and two are non-prehensile.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x12.png) 

Figure 14: Percentage of hands that were shown to perform a skill from the respective skill category.

##### Correlation analysis

Table [2](#S4.T2 "Table 2 ‣ Correlation analysis ‣ 4.2.2 Synthesis of results ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?") summarizes the correlation analysis. None of the correlations were significant.

Table 2: Correlation analysis of mechanism features vs. manipulated DoF in in-hand manipulation categories.

##### Analysis of extreme cases

Outliers that we identified in Figure [15](#S4.F15 "Figure 15 ‣ Analysis of extreme cases ‣ 4.2.2 Synthesis of results ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?") are (1) \[[12](#bib.bib12)\]with 2 fingers, 2 DoF, 1 actuator, and 3 controllable DoF of the object, as well as (2) the following examples of 6 controllable DoF of the object: two hands of \[[66](#bib.bib66)\] with 3 fingers, 7 DoF, 4 actuators, and 4 fingers, 8 DoF, 4 actuators respectively, and \[[55](#bib.bib55)\] with 4 fingers, 8 DoF, 4 actuators.

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x13.png) 

Figure 15: Number of actuators versus degrees of freedom that could be controlled in one of the in-hand manipulation categories. Extreme cases: (1) 3 controllable DoF of the object: \[[12](#bib.bib12)\] with one actuator (2 fingers, 2 DoF); (2) 6 controllable DoF of the object: two hands of \[[66](#bib.bib66)\] with four actuators (3 fingers, 7 DoF; 4 fingers, 8 DoF), and \[[55](#bib.bib55)\] with four actuators (4 fingers, 8 DoF).

### 4.3 Discussion

#### 4.3.1 Summary of evidence

##### Distribution of hand and sensor features

In Figure [13](#S4.F13 "Figure 13 ‣ Histogram of hand and sensor features ‣ 4.2.2 Synthesis of results ‣ 4.2 Results ‣ 4 Systematic Review of Robotic Hands and their Skill Repertoire ‣ Do Robots Really Need Anthropomorphic Hands?"), we can see that the publications are approximately evenly distributed between one and four actuation features. The mode of the distribution over the number of sensors used is one, and several publications use none, which hints that the integration of sensor data in hand control is lacking. Most publications discuss hands with five fingers, mimicking the human hand. While the number of DoF seems almost evenly distributed, the number of actuators peaks at around five, with more than 20 publications in this bin and more than ten in the next bin, indicating that developers of hands reduce the control complexity in comparison to the human hand. The most prominent exception is the Shadow Dexterous Hand, which has 20 actuators.

To conclude, the majority of the field aims at reproducing the look of the human hand by assembling five fingers, and some of them replicate all actuation features (palm, reposition/opposition of the thumb, flexion/extension, abduction/adduction), however, only a few reach the human hand’s DoF. Even fewer control these independently with individual actuators. There are only a few articles that focus on integrating complex hand mechanisms with multiple sensor sources.

##### Underexplored skill repertoire

Although the taxonomy used in this systematic review is designed to be independent of hand morphology \[[21](#bib.bib21)\], we observe that relatively few hands were evaluated across a diverse set of categories from this taxonomy. This observation applies to both complex hands and simple grippers. Specifically, if in-hand manipulation skills are investigated, these only control a few DoF of the object.

##### No correlation between hand and skill complexity

We could not find a correlation between hand complexity and the DoFs of an object that the hand is able to manipulate.

##### Simple mechanisms can be sufficient

We focused on the outliers \[[12](#bib.bib12), [66](#bib.bib66), [55](#bib.bib55)\] and found that they can control many DoF of an object without complex mechanisms.

#### 4.3.2 Limitations

The range and complexity of possible manipulation tasks are virtually impossible to quantify. While we have seen that simple hand mechanisms can control many DoF of an object, we cannot say that there is no better way of measuring task complexity, in which these mechanisms are worse than anthropomorphic hands. A better approach could be to measure the range of motion and other skill-specific performance criteria. We are unable to extract these from all publications in a comparable manner. There is also no notion of complexity in the other skill categories that we analyzed (e.g., signing could be thumbs up or complex sign language).

#### 4.3.3 Conclusions

The overall complexity of integrated hand mechanisms and sensors does not yet reach the level of human capabilities. Specifically, the integration of many sensors and complex mechanisms is underexplored. It is technically feasible to assemble a Shadow Dexterous Hand with tactile sensors and use a camera, but it is challenging to control intelligently.

The entire skill repertoire of most hands remains underexplored, and we recognize a need for more thorough and standardized evaluation of both new hands and existing hands.

There is no correlation between hand complexity and skill complexity for probably two reasons:

(1) The most complex hands in the analyzed studies (5 fingers, \>20\>20 degrees of freedom, and \>12\>12 actuators) were often capable of more complex in-hand manipulation skills than demonstrated. However, most studies use these hands to manipulate 1–3 degrees of freedom only. Just four exceptions manipulate ≥4\\geq 4 DoF of an object.

(2) Simple, non-anthropomorphic mechanisms are sufficient to manipulate more degrees of freedom than we expected, as demonstrated by the identified outliers \[[12](#bib.bib12), [66](#bib.bib66), [55](#bib.bib55)\]. When analyzing these more closely, we see that \[[12](#bib.bib12)\] use the simplest possible gripper design with two fingers, two DoF, and one actuator. They use the environment intelligently as an additional contact point to manipulate the object, which could be interpreted as using an additional virtual finger. \[[66](#bib.bib66)\] and \[[55](#bib.bib55)\] use non-anthropomorphic designs. Their hands have four fingers arranged in a circular shape around a center point, so that an object can be controlled from four different directions and enabling control of six DoF during in-hand manipulation.

## 5 Discussion

We compared the mechanical, sensory, and motor control features of the human hand with those of robotic hands to address the question of whether robotic hands should be designed to mimic the human hand.

### 5.1 Mechanical Features of the Human Hand

While robots are still inferior to humans in terms of sensory feedback, control, and learning, the case is not as clear-cut in terms of mechanical features. However, the question of whether researchers in robotics should aim to replicate the human model remains. This question can be addressed from multiple perspectives. Concerning the mechanical features or appearance, we choose to approach it by the number of fingers. So the question becomes more concrete:

##### The case for two fingers

Many tasks can be solved by simple mechanisms that have two fingers and one actively controlled degree of freedom. The gripper of \[[12](#bib.bib12)\] that can perform in-hand manipulation with 3 DoF by using the environment as a third contact surface in a clever way. \[[54](#bib.bib54)\] build upon this idea. Similarly, humans constantly exploit environment constraints \[[20](#bib.bib20)\]. For this to be possible, robotic hands must be robust, i.e., flexible and soft, with complexity shifting to intelligent motor control and sensor integration. \[[95](#bib.bib95)\] argue that animals that lack complex hands are still capable of complex manipulation. For instance, birds can use their bills to grasp, regrasp, and adjust the grasp of objects to establish a stable grip and gather information about the object, as well as exhibit complex behavior, such as building nests. \[[63](#bib.bib63)\] observe in experiments that many human grasps can be performed with the thumb and a single virtual finger. Additional DoFs in the human hand were only necessary for precision grasps, which are used less often in activities of daily living.

##### The case for three fingers

An additional finger is sometimes needed. Parrots have a tongue with which they can rotate objects in their bills or stabilize them during manipulation \[[95](#bib.bib95)\], essentially realizing 1 DoF in-hand manipulation with three finger-like body parts. Similarly, \[[121](#bib.bib121)\] found that the three-fingered BarrettHand can perform functional grasps to use tools such as an electric drill or a flashlight. \[[1](#bib.bib1)\] provide further evidence that three fingers are sufficient for most tasks. They use the grasp taxonomy of \[[24](#bib.bib24)\] to analyze the force distribution among fingers and palm in human grasps and found that only three fingers exert force in most cases. Other fingers are only used to fine-tune the grasp. Furthermore, \[[25](#bib.bib25)\] show that two or three fingers have an increased workspace volume and rotational range when compared to more fingers for the specific case of in-hand precision manipulation of circular objects.

Even in domains where we would expect multi-fingered hands to excel, the evidence is not clear. We present examples from deformable object manipulation and multi-object grasping.

Deformable objects constantly deform under external forces, e.g., the forces applied by a robotic hand. The more actively controllable contact points or surfaces a gripper has with a deformable object, the more control it has over the object’s shape. Interestingly, \[[83](#bib.bib83)\] found that much research on deformable objects has been conducted with two fingers and they suggest that using more fingers allows for finer control. This motivated \[[22](#bib.bib22)\] to develop a gripper for the tasks of picking up and placing folded clothes, folding a t-shirt in the air, and tracing an edge of a grasped cloth. They found that using three fingers with one finger opposing two others is particularly useful for the task of picking and placing folded clothes as abduction of the two fingers at the bottom creates a large support surface for the clothes that would otherwise collapse around a thin support surface. Hence, even in this domain, in which we assume that more fingers and DoFs are better, three fingers may be sufficient.

\[[96](#bib.bib96)\] distinguish twelve multi-object grasp types from human demonstrations and a robot grasping data set, in which eight different object types were grasped. They replicated many of these grasps using a BarrettHand with three fingers, which demonstrates that three fingers can be sufficient for complex grasps involving multiple objects. However, in some cases, this was not possible, e.g., the inverse basket grasp, in which five fingers form a basket around the objects and apply grip force, and the multi-finger pinch grasp, in which multiple pinch grasps were used simultaneously on multiple objects.

These observations suggest that a wide variety of manipulation tasks, including simple in-hand manipulation, can be solved with two fingers or at most three fingers for additional grasp stabilization during manipulation or tool use. However, \[[95](#bib.bib95)\] note that birds make use of a highly flexible neck that functions as an equivalent to the human wrist during manipulation, and \[[62](#bib.bib62)\] make the equivalent observation in human manipulation with restricted DoFs in their hand. Robotic wrists are often not as flexible, and orientation changes often require large repositioning of the arm, which makes operation in restricted workspaces difficult.

##### The case for four fingers

\[[66](#bib.bib66)\] and \[[55](#bib.bib55)\] use a non-anthropomorphic design with two pairs of opposing fingers so that 6 DoF of an object can be controlled during in-hand manipulation. This mechanism can be equally dexterous as an anthropomorphic hand and might even be better suited for specific in-hand manipulation tasks.

##### The case for more than five fingers

Humans use two hands for many tasks. An example of a complex manipulation task is tying shoe laces, which requires two pairs of opposing fingers. \[[59](#bib.bib59)\] report that individuals with six fully functional fingers can solve this task with only one hand. As the research of \[[96](#bib.bib96)\] on multi-object grasps suggests, more fingers allow handling multiple objects simultaneously and conforming better with the shape of multiple objects. We conclude that the more tasks that have to be solved in parallel, the more fingers are required. Complex in-hand manipulation can benefit from more fingers, and human in-hand manipulation is likely limited not just by the degrees of freedom per finger and range of motion per joint, but also by the number of fingers, as has been demonstrated by \[[59](#bib.bib59)\].

##### Summary

How many fingers should we use? Almost certainly, robots do not need five fingers like the human hand. Currently, there is no evidence that five fingers are optimal. This raises questions about which configuration is most effective. Two fingers can be sufficient for many tasks. Moreover, the range of tasks can even be extended with the effective use of environment contacts. Three fingers are a good compromise between dexterity and simplicity, as they improve stability and enable tool use. A flexible wrist significantly enhances manipulation capabilities considerably for two and three fingers. Four fingers provide more dexterity for in-hand manipulation, and with two more fingers, we found evidence of increasing dexterity. If and how more fingers can be used to improve robotic manipulation remains an open question.

#### 5.1.1 Do we need an opposable thumb?

The thumb is the most independently controlled of the human fingers \[[33](#bib.bib33)\]. An opposable thumb improves the prehensile function of a hand compared to parallel fingers, as it allows us to exert forces on an object from opposing directions. However, a robotic hand does not necessarily need a thumb that reflects the function and shape of the human thumb. Parallel jaw grippers, featuring two opposing fingers, are capable of producing stable grasps. It is not even necessary to have more than one finger to apply forces from opposing directions, e.g., it is possible to hold an object between one finger and a palm, or an octopus arm can wrap around an object. The BarrettHand has three fingers, and two of them can rotate 180 degrees around their base. This capability enables configurations in which one finger is opposing the others, in which all three fingers are equally distributed around the object, or in which all fingers are parallel. \[[8](#bib.bib8)\] point out that the human thumb creates an asymmetry and constrains the orientation of the hand. They entertain the idea of designing hands with more than one opposing finger to enable more dexterous in-hand manipulation, which would usually require two hands. There are examples of such hands with two pairs of opposing fingers \[[66](#bib.bib66), [55](#bib.bib55)\].

In conclusion, it is necessary to exert opposing forces; however, the human example is by no means the only solution, and it is most likely not the best either. We suggest exploring the use of more than one pair of opposing fingers for complex tasks. If simplicity is preferred, mechanisms such as the BarrettHand, which allow the exertion of opposing forces, are sufficient.

#### 5.1.2 Do we need so many degrees of freedom, including abduction/adduction and three flexion/extension joints per finger, and do they need to be individually controllable?

Comparing independent finger movements of humans versus monkeys, \[[30](#bib.bib30)\] found that individuation is higher in human subjects. Specifically, they found that the thumb and index fingers are the most independently moving fingers, while the ring and middle fingers are most coupled with the movement of other fingers. This observation coincides with the fact that the thumb, index finger, and little finger have more muscles for individual actuation of these fingers. The humans’ greater independence of finger movements in comparison to macaques, for instance, arises from anatomical differences such as splitting of a separate muscle belly and tendons, and a loss of tendons in multitendoned muscles \[[30](#bib.bib30)\], but also from finer representation in the primary motor cortex. Nevertheless, humans still often do not control each finger independently. \[[30](#bib.bib30)\] found that the angular motion mostly happens in the middle joint of each finger (usually PIP joint, MCP for the thumb). This observation indicates that a reduced set of actively controlled flexion joints might be sufficient.

By constraining individual fingers of human subjects during manipulation experiments, \[[63](#bib.bib63)\] explored the relevance of independent fingers in activities of daily living. Their results suggest that the precision grasps of the human hand with small contact areas rely on independent abduction/adduction of the fingers more than on independent flexion/extension, as this allows for precise opposition of the thumb.

In conclusion, a robotic hand does not necessarily need 24 DoFs. However, abduction/adduction support precise manipulation, and the middle joints of the fingers should be actuated, while the other flexion joints could be passive. A multi-fingered hand should have three individually controlled fingers.

#### 5.1.3 Do we need a large active and even larger passive range of motion?

Not many authors touch this topic. Based on the literature we analyzed, we cannot provide a conclusive answer.

#### 5.1.4 Do we need a soft and deformable surface, particularly at the large surface of the flexible palm?

\[[1](#bib.bib1)\] measure the distribution of forces for different grasp types. Although the only force sensors on the palm that they use are below the little finger, their heatmaps suggest that the palm is important for human grasps. The benefit of flexible and soft hands is twofold: (1) contact with the environment does not damage the hardware, and (2) support of prehension by adaptation to the shape of objects. Humans do not avoid contact with the environment during manipulation; they actively use it and exploit environmental constraints. For example, when grasping a flat object from a table, they often slide it to the edge to grasp it more easily \[[20](#bib.bib20)\].

#### 5.1.5 Do we need the ability to produce high grip forces in combination with dexterity?

While we can roughly match the degrees of freedom and number of fingers of a human hand, we are not yet able to match the force-to-weight ratio in dexterous hands. In principle, a higher force-to-weight ratio is desirable, but only if it does not compromise other performance factors such as speed, precision, or compliance. In many applications, especially those relying on form closure or simple grasps, high grip force may not be necessary. Instead, low-force, lightweight, and mechanically simple three-fingered designs are often sufficient and even preferable due to their robustness, lower cost, and ease of control. The key trade-off lies in determining whether the added force capacity truly enhances task performance or whether it introduces unnecessary complexity and compromises overall hand functionality.

### 5.2 Sensors of the Human Hand

As introduced earlier, robots are still inferior to humans in terms of sensory feedback. We also presented some examples of the implementation of complex skills with current robot hands and discussed the case of teleoperation, which suggests that cognition appears to be the primary constraint rather than hardware and sensing. For instance, surgeons accomplish remarkable tasks with parallel grippers and no haptic feedback. However, this ability depends on extensive training and experience to compensate for limited feedback and comes at the cost of increased cognitive load \[[72](#bib.bib72)\].

Moreover, from our systematic review, we can see that the mode of the distribution over the number of sensors used is one, and several publications use none, which hints that the integration of sensor data in robotic hand control is lacking. There are only a few articles that focus on integrating complex hand mechanisms with multiple sensor sources. Thus, we cannot provide conclusive answers for this section; nevertheless, we attempt to provide some indications.

This raises the question of whether advanced robotic hands should integrate haptic perception and, if so, to what extend? To address this question more concretely and provide actionable recommendations to practitioners, we subdivide these questions into the advantages and disadvantages of haptic feedback and then analyze the most relevant aspects of sensory feedback.

#### 5.2.1 Is visual feedback enough?

Visual feedback plays a significant role in dexterous manipulation, as it provides crucial information about the external environment and the object’s spatial properties. For instance, visual information is critical for coordinating hand movements with external objects, especially in dynamic environments \[[50](#bib.bib50)\]. However, relying solely on visual feedback may not be sufficient for optimal performance in many situations, because in situations where vision is impaired or obstructed, relying solely on visual feedback can lead to significant performance decrements \[[36](#bib.bib36)\]. Relying entirely on visual feedback increases cognitive load and can slow down processing speed, as visual information must be interpreted and translated into action \[[72](#bib.bib72)\]. The computational cost is also significant in the case of robots \[[29](#bib.bib29)\].

#### 5.2.2 What are the benefits of haptic perception?

Proprioception provides crucial information about the position and movement of limbs \[[53](#bib.bib53)\], enabling coordinated hand movements and precise timing in complex tasks. Tactile feedback enables finer control over grip force and manipulation precision. It helps individuals adjust their grip in real-time to prevent dropping or crushing objects \[[35](#bib.bib35)\]. The combination of tactile and proprioceptive feedback allows humans to adapt to varying textures, weights, and other properties of objects in a dynamic environment \[[53](#bib.bib53)\].

#### 5.2.3 Do we need proprioceptive feedback?

Proprioception provides continuous information about the position and movement of joints and limbs \[[53](#bib.bib53)\], which is vital for coordinating complex hand movements. Thus, impairments in proprioception can lead to inaccurate limb positioning and movement trajectories \[[27](#bib.bib27)\], making precise manipulation difficult. It aids in motor learning by providing feedback that helps refine motor actions and adjust movements based on sensory information \[[82](#bib.bib82)\].

#### 5.2.4 Do we need tactile feedback?

Tactile feedback enables the precise control and modulation of grip force, allowing individuals to dynamically adjust grip pressure to prevent object slippage or damage \[[35](#bib.bib35)\]. It enables the detection of an object’s texture and other surface properties, which are essential for determining the appropriate grip strategy and ensuring secure handling \[[53](#bib.bib53)\]. Tactile feedback plays a crucial role in object recognition and differentiation by providing information about shape, size, and material properties when visual inputs are limited \[[53](#bib.bib53)\].

#### 5.2.5 How much resolution or accuracy is required?

Only 62 articles include proprioceptive perception in their setup, but not all use it to perform the skills. Of those 62 articles, only 18 articles use tactile perception to implement the skills, from which 7 use it as a binary or average contact signal. Thus, we cannot provide a conclusive answer or guidelines regarding the ideal spatial, temporal, or force resolution required to improve dexterity.

#### 5.2.6 Do robots need thermoreceptors?

Thermoreceptors allow for the detection of temperature changes in objects being manipulated, which can be useful to discriminate between materials \[[7](#bib.bib7)\]. Robots have also been shown to benefit from thermal perception \[[7](#bib.bib7)\].

#### 5.2.7 Do robots need nociceptors?

Nociceptors play a crucial role in detecting harmful stimuli and triggering reflexive responses to prevent injury. In robotics, incorporating nociception could extend robot lifespan, reduce maintenance needs, and enhance safety by recognizing harmful interactions. Additionally, nociception may enhance a robot’s positioning speed and accuracy \[[69](#bib.bib69), [68](#bib.bib68)\], although its specific impact on manipulation tasks requires further study. Additionally, nociception could foster biologically like behaviors and increase the non-verbal interpretability of robot behavior. However, building specific nociceptors in robots may not be necessary, as they could be represented by a combination of other sensory modalities.

#### 5.2.8 What would be more important for robots: proprioceptive and tactile feedback?

Both systems provide critical information, but proprioceptive and tactile feedback offer distinct types of insights. These differences can significantly influence specific manipulation capabilities, as each system supports different functions during manipulation.

Proprioceptive feedback provides essential information about the position and movement of limbs and joints. It is essential to coordinate complex hand movements efficiently \[[53](#bib.bib53)\]. This feedback is crucial for maintaining stability and coordination. These are both needed for precise and controlled manipulation, especially when visual feedback is limited. Proprioception plays a central role in motor learning and adaptation, enabling individuals to refine their movements and adjust to new tasks.

Tactile feedback is crucial for detecting the texture and material properties of objects. It enables fine discrimination between different surfaces, which is vital for manipulation tasks \[[53](#bib.bib53)\]. Tactile feedback provides important cues for modulating grip force, preventing slippage, and ensuring secure handling of objects. Tactile sensors provide instant feedback about contact with objects. This facilitates real-time adjustments essential for dynamic tasks \[[53](#bib.bib53)\]. For dexterous manipulation, such as material handling, texture discrimination, or grip force precision, tactile feedback is a more advantageous complement to visual feedback than proprioception.

## 6 Conclusion

In the previous section, we provided recommendations for designing robotic hands. For prosthetics, emulating the mechanical characteristics of the human hand is a sensible goal. For robots, however, this is less applicable. With intelligent control strategies, even simple two- or three-fingered grippers can perform tasks effectively, for example, by leveraging the environment to counteract forces from other directions. We can even go beyond human manipulation abilities. More complex, non-anthropomorphic hands can solve complex manipulation problems more easily or multiple problems simultaneously because they can directly control many DoFs of one or multiple objects without repositioning the hand. They could also solve various manipulation tasks simultaneously. However, how this can be done remains an open question.

However, are we, as roboticists, actually looking at the right defining characteristics of human hands? While we can roughly match the degrees of freedom and number of fingers of a human hand, we are not yet able to match the force-to-weight ratio in dexterous hands. This fact is well-known, but this may not be the most interesting aspect of a human hand. We assume that learning and control are a large part of what is currently missing for human-like dexterity. However, learning is a form of iteratively improving stochastic control that is only possible with robust hardware. The human hand is soft, deformable, and flexible, with a larger passive range of motion, which makes it particularly robust and suited for approximate control and manipulation under environmental uncertainty. We argue that we optimized hand designs for the wrong characteristics of human hands in the past. We can perform complex skills with three or four fingers and fewer degrees of freedom. Robustness to environmental conditions should be the focus of hand design.

The synergetic combination of mechanical aspects, perception, and control might be more important for a robotic hand to match and potentially surpass human dexterity than anthropomorphic kinematics alone. Teleoperation demonstrates that the most limiting factor currently is the cognitive ability of robotic systems, as surgeons can perform complex procedures using simple grippers and tools without haptic feedback. However, haptic feedback, even in its current state of development, has a significant overall effect on measures of applied forces, completion time, accuracy, and success rates \[[5](#bib.bib5)\].

Our systematic review reveals a key shortcoming: most hands are tested within only a few categories of Dollar’s taxonomy \[[21](#bib.bib21)\], and even within these categories, there is limited variety. This lack of comprehensive evaluation is especially evident in cases of complex hands, which are seldom tested for in-hand manipulation. To address this, the field needs robust evaluation protocols that can assess complete mechanism-sensor-software systems across all skill categories and complexity levels. Such protocols must demonstrate a hand’s mechanical and functional capabilities, especially by requiring the intelligent use of advanced sensors. For example, to truly evaluate the benefits of tactile sensors, protocols should include complex manipulation tasks that demand fine motor control. Establishing these benchmarks is crucial for making meaningful comparisons of hand designs and for guiding progress in robotic hand development.

## Declarations

\\bmhead

Funding This work was supported by the European Commission under the Horizon 2020 framework program for Research and Innovation via the APRIL project (project number: 870142) and by the Vibro-Sense Project (project number: 03DPS1242A) funded by the Bundesministerium Forschung, Technologie und Raumfahrt (BMFTR) under the DATIpilot program. Open Access funding provided by the Projekt DEAL (Open access agreement for Germany). \\bmheadConflict of interest/Competing interests The authors declare that they have no conflict of interest. \\bmheadEthics approval This article does not contain any studies with human participants or animals performed by any of the authors.

\\bmhead

Open Access This article is licensed under a Creative Commons Attribution 4.0 International License, which permits use, sharing, adaptation, distribution, and reproduction in any medium or format, as long as you give appropriate credit to the original author(s) and the source, provide a link to the Creative Commons license, and indicate if changes were made. The images or other third-party material in this article are included in the article’s Creative Commons license, unless indicated otherwise in a credit line to the material. If material is not included in the article’s Creative Commons license and your intended use is not permitted by statutory regulation or exceeds the permitted use, you will need to obtain permission directly from the copyright holder. To view a copy of this license, visit <http://creativecommons.org/licenses/by/4.0/>.

\\bmhead

Consent to participate Not applicable \\bmheadConsent for publication/Informed consent Not applicable \\bmheadAvailability of data and materials Overviews of the analyzed robotic hands and the papers considered for the systematic review are available at <https://figshare.com/s/f4fdd9aca1c134f010dd>. \\bmheadCode availability Code for filtering and plotting in the systematic review will be provided for the camera-ready version of this manuscript.

## Appendix A Radar Diagram of Skills

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x14.png)

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2508.05415/assets/x15.png)

Figure 16: Radar diagram of some selected skills.

Figure [16](#A1.F16 "Figure 16 ‣ Appendix A Radar Diagram of Skills ‣ Do Robots Really Need Anthropomorphic Hands?") shows a radar diagram for manipulation skills similar to ones in Figure [8](#S3.F8 "Figure 8 ‣ 3.1 Mechanics ‣ 3 Robotic Hands ‣ Do Robots Really Need Anthropomorphic Hands?") for robotic and prosthetic hands. The following skills are displayed. We explain the human way of implementing them. This is by no means a scientifically grounded exact study, however, it gives an intuitive idea of the required complexity of the mechanisms to realize these skills.

- •  
Open handed holding: Only a large support surface like the palm of the human hand is needed to hold an object. No joints are necessary.
- •  
Pointing / pushing: With an extended index finger and all other fingers flexed, the index finger points in the direction of an object of interest (pointing) or pushes an object, e.g., on a table in some desired direction (pushing).
- •  
Scratching: With an index finger, we can scratch on a surface with flexion in only one joint.
- •  
Grasping / holding: We can grasp smaller objects just with the thumb and index finger by bringing them closer to the object, e.g., by flexion of the index finger.
- •  
Flipping a page: We need two fingers to grasp a page of a book, maybe separate it from other pages (e.g., by extension of the thumb and flexion of the index finger), and turn it around.
- •  
Thumbs up gesture: With the thumb in reposition, we can make this gesture by extending one joint of the thumb. The gesture only makes sense if we can make a fist through flexion of at least another finger.
- •  
Handwriting: With the thumb on the side of the index finger, we can hold a pen between thumb, index finger, and middle finger by flexing the thumb. Control of the pen in a plane can be achieved with flexion/extension of the thumb and abduction/adduction of the index and middle finger in one direction as well as flexion in all three fingers in another direction.
- •  
Using a screw driver: In order to use a screw driver effectively, we hold it between thumb, index finger, middle finger, and palm. The ring finger can support the screw driver close to the palm when flexed. We can rotate the screw driver with thumb and middle finger, but when the middle finger has to go back to the initial position, the index finger has to hold the screw driver. The rotation can be realized with the reposition/opposition and flexion/extension of the thumb, as well as flexion/extension and minor abduction/adduction of the middle finger. The supporting index finger can make and break contact through flexion.
- •  
Sign language: For ”I love you” in American sign language, five fingers are usually required, these have to provide flexion/extension DOFs, and the thumb has to be in reposition.
- •  
Button up: Two hands are needed to button up a shirt. While we can hold the button between thumb and index finger, it is easier to control the shirts shape with thumb, index finger, and middle finger of the other hand. Flexion/extension for all of these fingers is necessary. In addition, with reposition/opposition control of both thumbs, we have enough degrees of freedom for fine control of the shirt and button.
- •  
False cut (magic trick): False cuts are card tricks. Although cards are handled as stacks, for some tricks it is necessary to handle three stacks of cards at the same time. This is usually done with two hands so that 2–4 points of contact between the hands and the stack of cards exist. For example, the right hand holds one stack of cards between little finger, ring finger, and thumb, the left hand holds one stack between base of the thumb, palm, ring finger, and little finger, a third stack of cards is manipulated with the left index and middle finger and the right index and middle finger. A rotational movement to the third stack of cards can be created by finger movements or movements of the wrist and forearm. Precise opposition of fingers (e.g., thumb and ring finger of the right hand in the previous example) is necessary, hence, abduction/adduction as well as reposition/opposition is needed. To grasp and hold the stacks, flexion/extension is needed. A minimum of eight fingers is required in this example and a similar number of degrees of freedom.

## References

- \\bibcommenthead
- Abbasi et al. \[2016\] Abbasi B, Noohi E, Parastegari S, et al (2016) Grasp Taxonomy Based on Force Distribution. In: IEEE International Symposium on Robot and Human Interactive Communication (RO-MAN), New York, NY, USA, pp 1098–1103, [10.1109/ROMAN.2016.7745245](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ROMAN.2016.7745245)
- Abd et al. \[2022\] Abd MA, Ingicco J, Hutchinson DT, et al (2022) Multichannel Haptic Feedback Unlocks Prosthetic Hand Dexterity. Sci Rep 12(1):2323\. [10.1038/s41598-022-04953-1](https://ar5iv.labs.arxiv.org/doi.org/10.1038/s41598-022-04953-1)
- Alfadhel and Kosel \[2015\] Alfadhel A, Kosel J (2015) Magnetic Nanocomposite Cilia Tactile Sensor. Adv Mater 27(47):7888–7892\. [10.1002/adma.201504015](https://ar5iv.labs.arxiv.org/doi.org/10.1002/adma.201504015)
- Appell and Stang-Voss \[2008\] Appell HJ, Stang-Voss C (2008) Funktionelle Anatomie: Grundlagen sportlicher Leistung und Bewegung, 4th edn. Springer, [10.1007/978-3-540-74864-9](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-3-540-74864-9)
- Bergholz et al. \[2023\] Bergholz M, Ferle M, Weber BM (2023) The Benefits of Haptic Feedback in Robot Assisted Surgery and Their Moderators: A Meta-Analysis. Sci Rep 13(1):19215\. [10.1038/s41598-023-46641-8](https://ar5iv.labs.arxiv.org/doi.org/10.1038/s41598-023-46641-8)
- Bernshtein \[1967\] Bernshtein NA (1967) The Co-Ordination and Regulation of Movements. Pergamon Press
- Bhattacharjee et al. \[2021\] Bhattacharjee T, Clever HM, Wade J, et al (2021) Material Recognition via Heat Transfer Given Ambiguous Initial Conditions. IEEE Trans Haptics 14(4):885–896\. [10.1109/TOH.2021.3089990](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TOH.2021.3089990)
- Billard and Kragic \[2019\] Billard A, Kragic D (2019) Trends and Challenges in Robot Manipulation. Science 364(6446):eaat8414\. [10.1126/science.aat8414](https://ar5iv.labs.arxiv.org/doi.org/10.1126/science.aat8414)
- Bonner et al. \[2021\] Bonner LER, Buhl DD, Kristensen K, et al (2021) AU Dataset for Visuo-Haptic Object Recognition for Robots. Dataset Description arXiv:2112.13761, Aarhus University, Denmark, [10.6084/m9.figshare.14222486](https://ar5iv.labs.arxiv.org/doi.org/10.6084/m9.figshare.14222486)
- Brandes et al. \[2019\] Brandes R, Lang F, Schmidt RF (eds) (2019) Physiologie des Menschen: mit Pathophysiologie, 32nd edn. Springer-Lehrbuch, Springer
- Büscher et al. \[2015\] Büscher GH, Kõiva R, Schürmann C, et al (2015) Flexible and Stretchable Fabric-Based Tactile Sensor. Rob Auton Syst 63, Part 3:244–252\. [10.1016/j.robot.2014.09.007](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.robot.2014.09.007)
- Chavan-Dafle et al. \[2020\] Chavan-Dafle N, Holladay R, Rodriguez A (2020) Planar in-Hand Manipulation Via Motion Cones. Int J Rob Res 39(2-3):163–182\. [10.1177/0278364919880257](https://ar5iv.labs.arxiv.org/doi.org/10.1177/0278364919880257)
- Chi et al. \[2018\] Chi C, Sun X, Xue N, et al (2018) Recent Progress in Technologies for Tactile Sensors. Sensors 18(4):948\. [10.3390/s18040948](https://ar5iv.labs.arxiv.org/doi.org/10.3390/s18040948)
- Clark et al. \[2020\] Clark MA, Choi JH, Douglas M (2020) Biology 2e, 2nd edn. XanEdu Publishing Inc.
- Cobos et al. \[2008\] Cobos S, Ferre M, Sanchez Uran M, et al (2008) Efficient Human Hand Kinematics for Manipulation Tasks. In: IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Nice, France, pp 2246–2251, [10.1109/IROS.2008.4651053](https://ar5iv.labs.arxiv.org/doi.org/10.1109/IROS.2008.4651053)
- Controzzi et al. \[2014\] Controzzi M, Cipriani C, Carrozza MC (2014) Design of Artificial Hands: A Review. In: The Human Hand as an Inspiration for Robot Hand Development, Springer Tracts in Advanced Robotics, vol II. Springer International Publishing, p 219–246
- Dahiya and Valle \[2013\] Dahiya RS, Valle M (2013) Tactile Sensing: Definitions and Classification. In: Robotic Tactile Sensing. Springer Netherlands, p 13–17, [10.1007/978-94-007-0579-1\_2](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-94-007-0579-1%5F2)
- Dahiya et al. \[2010\] Dahiya RS, Metta G, Valle M, et al (2010) Tactile Sensing – From Humans to Humanoids. IEEE Trans Robot 26(1):1–20\. [10.1109/TRO.2009.2033627](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TRO.2009.2033627)
- Dahiya et al. \[2013\] Dahiya RS, Mittendorfer P, Valle M, et al (2013) Directions Toward Effective Utilization of Tactile Skin: A Review. IEEE Sens J 13(11):4121–4138\. [10.1109/JSEN.2013.2279056](https://ar5iv.labs.arxiv.org/doi.org/10.1109/JSEN.2013.2279056)
- Della Santina et al. \[2017\] Della Santina C, Bianchi M, Averta G, et al (2017) Postural Hand Synergies During Environmental Constraint Exploitation. Front Neurorobot 11(41). [10.3389/fnbot.2017.00041](https://ar5iv.labs.arxiv.org/doi.org/10.3389/fnbot.2017.00041)
- Dollar \[2014\] Dollar AM (2014) Classifying Human Hand Use and the Activities of Daily Living. In: The Human Hand as an Inspiration for Robot Hand Development. Springer Tracts in Advanced Robotics, Springer International Publishing, Cham, p 201–216, [10.1007/978-3-319-03017-3\_10](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-3-319-03017-3%5F10)
- Donaire et al. \[2020\] Donaire S, Borràs J, Alenyà G, et al (2020) A Versatile Gripper for Cloth Manipulation. IEEE Robot Autom Lett 5(4):6520–6527\. [10.1109/LRA.2020.3015172](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2020.3015172)
- Faisal et al. \[2008\] Faisal AA, Selen LPJ, Wolpert DM (2008) Noise in the Nervous System. Nat Rev Neurosci 9(4):292–303\. [10.1038/nrn2258](https://ar5iv.labs.arxiv.org/doi.org/10.1038/nrn2258)
- Feix et al. \[2015\] Feix T, Bullock IM, Gloumakov Y, et al (2015) Rotational Ranges of Human Precision Manipulation When Grasping Objects with Two to Five Digits. In: Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC), Milan, Italy, pp 5785–5790, [10.1109/EMBC.2015.7319707](https://ar5iv.labs.arxiv.org/doi.org/10.1109/EMBC.2015.7319707)
- Feix et al. \[2021\] Feix T, Bullock IM, Gloumakov Y, et al (2021) Effect of Number of Digits on Human Precision Manipulation Workspaces. IEEE Trans Haptics 14(1):68–82\. [10.1109/TOH.2020.3003556](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TOH.2020.3003556)
- Franklin and Wolpert \[2011\] Franklin DW, Wolpert DM (2011) Computational Mechanisms of Sensorimotor Control. Neuron 72(3):425–442\. [10.1016/j.neuron.2011.10.006](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.neuron.2011.10.006)
- Ghez et al. \[1995\] Ghez C, Gordon J, Ghilardi MF (1995) Impairments of Reaching Movements in Patients Without Proprioception. II. Effects of Visual Information on Accuracy. J Neurophysiol 73(1):361–372\. [10.1152/jn.1995.73.1.361](https://ar5iv.labs.arxiv.org/doi.org/10.1152/jn.1995.73.1.361)
- Glazier et al. \[2003\] Glazier PS, Davids K, Bartlett RM (2003) DYNAMICAL SYSTEMS THEORY: A Relevant Framework for Performance-Oriented Sports Biomechanics Research,. Sport Science 7:1–8
- Goyal et al. \[2023\] Goyal A, Xu J, Guo Y, et al (2023) RVT: Robotic View Transformer for 3D Object Manipulation. In: Conference on Robot Learning (CoRL), vol 229\. PMLR, pp 694–710
- Häger-Ross and Schieber \[2000\] Häger-Ross C, Schieber MH (2000) Quantifying the Independence of Human Finger Movements: Comparisons of Digits, Hands, and Movement Frequencies. J Neurosci 20(22):8542–8550\. [10.1523/JNEUROSCI.20-22-08542.2000](https://ar5iv.labs.arxiv.org/doi.org/10.1523/JNEUROSCI.20-22-08542.2000)
- Hellebrekers et al. \[2020\] Hellebrekers T, Chang N, Chin K, et al (2020) Soft Magnetic Tactile Skin for Continuous Force and Location Estimation Using Neural Networks. IEEE Robot Autom Lett 5(3):3892–3898\. [10.1109/LRA.2020.2983707](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2020.2983707)
- Huber et al. \[1997\] Huber JE, Fleck NA, Ashby MF (1997) The Selection of Mechanical Actuators Based on Performance Indices. Proc R Soc A: Math Phys Eng Sci 453(1965):2185–2205\. [10.1098/rspa.1997.0117](https://ar5iv.labs.arxiv.org/doi.org/10.1098/rspa.1997.0117)
- Ingram et al. \[2008\] Ingram JN, Körding KP, Howard IS, et al (2008) The Statistics of Natural Hand Movements. Exp Brain Res 188(2):223–236\. [10.1007/s00221-008-1355-3](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s00221-008-1355-3)
- Jamone et al. \[2015\] Jamone L, Natale L, Metta G, et al (2015) Highly Sensitive Soft Tactile Sensors for an Anthropomorphic Robotic Hand. IEEE Sens J 15(8):4226–4233\. [10.1109/JSEN.2015.2417759](https://ar5iv.labs.arxiv.org/doi.org/10.1109/JSEN.2015.2417759)
- Johansson and Flanagan \[2009\] Johansson RS, Flanagan JR (2009) Coding and Use of Tactile Signals from the Fingertips in Object Manipulation Tasks. Nat Rev Neurosci 10(5):345–359\. [10.1038/nrn2621](https://ar5iv.labs.arxiv.org/doi.org/10.1038/nrn2621)
- Johansson et al. \[1992\] Johansson RS, Häger C, Bäckström L (1992) Somatosensory Control of Precision Grip During Unpredictable Pulling Loads. Exp Brain Res 89(1):204–213\. [10.1007/BF00229017](https://ar5iv.labs.arxiv.org/doi.org/10.1007/BF00229017)
- Juiña Quilachamín and Navarro-Guerrero \[2023\] Juiña Quilachamín OA, Navarro-Guerrero N (2023) A Biomimetic Fingerprint for Robotic Tactile Sensing. In: International Symposium on Robotics (ISR Europe). VDE Verlag GmbH, pp 112–118, [10.48550/arXiv.2307.00937](https://ar5iv.labs.arxiv.org/doi.org/10.48550/arXiv.2307.00937)
- Jung et al. \[2015\] Jung Y, Lee DG, Park J, et al (2015) Piezoresistive Tactile Sensor Discriminating Multidirectional Forces. Sensors 15(10):25463–25473\. [10.3390/s151025463](https://ar5iv.labs.arxiv.org/doi.org/10.3390/s151025463)
- Kamat et al. \[2019\] Kamat AM, Pei Y, Kottapalli AGP (2019) Bioinspired Cilia Sensors with Graphene Sensing Elements Fabricated Using 3D Printing and Casting. Nanomaterials 9(7):954\. [10.3390/nano9070954](https://ar5iv.labs.arxiv.org/doi.org/10.3390/nano9070954)
- Kapandji \[1986\] Kapandji A (1986) Cotation clinique de l’opposition et de la contre-opposition du pouce. Ann Chir Main 5(1):67–73\. [10.1016/S0753-9053(86)80053-9](https://ar5iv.labs.arxiv.org/doi.org/10.1016/S0753-9053%2886%2980053-9)
- Kapandji \[2007\] Kapandji IA (2007) The Physiology of the Joints, 6th edn. Churchill Livingstone, Edinburgh ; New York
- Kappassov et al. \[2015\] Kappassov Z, Corrales JA, Perdereau V (2015) Tactile Sensing in Dexterous Robot Hands – Review. Rob Auton Syst 74, Part A:195–220\. [10.1016/j.robot.2015.07.015](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.robot.2015.07.015)
- Kavraki and LaValle \[2008\] Kavraki LE, LaValle SM (2008) Motion Planning. In: Springer Handbook of Robotics, vol Part A, 5\. Springer, p 109–131
- Kawato \[1999\] Kawato M (1999) Internal Models for Motor Control and Trajectory Planning. Curr Opin Neurobiol 9(6):718–727\. [10.1016/S0959-4388(99)00028-8](https://ar5iv.labs.arxiv.org/doi.org/10.1016/S0959-4388%2899%2900028-8)
- Ko et al. \[2017\] Ko T, Kaminaga H, Nakamura Y (2017) Underactuated Four-Fingered Hand with Five Electro Hydrostatic Actuators in Cluster. In: IEEE International Conference on Robotics and Automation (ICRA), Singapore, pp 620–625, [10.1109/ICRA.2017.7989077](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ICRA.2017.7989077)
- Körding and Wolpert \[2006\] Körding KP, Wolpert DM (2006) Bayesian Decision Theory in Sensorimotor Control. Trends Cogn Sci 10(7):319–326\. [10.1016/j.tics.2006.05.003](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.tics.2006.05.003)
- Kuppuswamy et al. \[2020\] Kuppuswamy N, Alspach A, Uttamchandani A, et al (2020) Soft-Bubble Grippers for Robust and Perceptive Manipulation. In: IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Las Vegas, NV, USA, pp 9917–9924, [10.1109/IROS45743.2020.9341534](https://ar5iv.labs.arxiv.org/doi.org/10.1109/IROS45743.2020.9341534)
- Kutch and Valero-Cuevas \[2011\] Kutch JJ, Valero-Cuevas FJ (2011) Muscle Redundancy Does Not Imply Robustness to Muscle Dysfunction. J Biomech 44(7):1264–1270\. [10.1016/j.jbiomech.2011.02.014](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.jbiomech.2011.02.014)
- Lambeta et al. \[2020\] Lambeta M, Chou PW, Tian S, et al (2020) DIGIT: A Novel Design for a Low-Cost Compact High-Resolution Tactile Sensor With Application to In-Hand Manipulation. IEEE Robot Autom Lett 5(3):3838–3845\. [10.1109/LRA.2020.2977257](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2020.2977257)
- Land and McLeod \[2000\] Land MF, McLeod P (2000) From Eye Movements to Actions: How Batsmen Hit the Ball. Nat Neurosci 3(12):1340–1345\. [10.1038/81887](https://ar5iv.labs.arxiv.org/doi.org/10.1038/81887)
- Larson et al. \[2016\] Larson C, Peele B, Li S, et al (2016) Highly Stretchable Electroluminescent Skin for Optical Signaling and Tactile Sensing. Science 351(6277):1071–1074\. [10.1126/science.aac5082](https://ar5iv.labs.arxiv.org/doi.org/10.1126/science.aac5082)
- Lederman and Klatzky \[1987\] Lederman SJ, Klatzky RL (1987) Hand Movements: A Window into Haptic Object Recognition. Cogn Psychol 19(3):342–368\. [10.1016/0010-0285(87)90008-9](https://ar5iv.labs.arxiv.org/doi.org/10.1016/0010-0285%2887%2990008-9)
- Lederman and Klatzky \[2009\] Lederman SJ, Klatzky RL (2009) Haptic Perception: A Tutorial. Atten Percept Psychophys 71(7):1439–1459\. [10.3758/APP.71.7.1439](https://ar5iv.labs.arxiv.org/doi.org/10.3758/APP.71.7.1439)
- Liang et al. \[2024\] Liang B, Ota K, Tomizuka M, et al (2024) Robust in-Hand Manipulation with Extrinsic Contacts. In: IEEE International Conference on Robotics and Automation (ICRA), pp 6544–6550, [10.1109/ICRA57147.2024.10611664](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ICRA57147.2024.10611664)
- Liarokapis and Dollar \[2019\] Liarokapis M, Dollar AM (2019) Combining Analytical Modeling and Learning to Simplify Dexterous Manipulation With Adaptive Robot Hands. IEEE Trans Autom Sci Eng 16(3):1361–1372\. [10.1109/TASE.2018.2885801](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TASE.2018.2885801)
- Liu et al. \[2020\] Liu Y, Li Z, Liu H, et al (2020) Bioinspired Embodiment for Intelligent Sensing and Dexterity in Fine Manipulation: A Survey. IEEE Trans Industr Inform 16(7):4308–4321\. [10.1109/TII.2020.2971643](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TII.2020.2971643)
- Lutz and Bensmaia \[2021\] Lutz OJ, Bensmaia SJ (2021) Proprioceptive Representations of the Hand in Somatosensory Cortex. Curr Opin Physiol 21:9–16\. [10.1016/j.cophys.2021.04.002](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.cophys.2021.04.002)
- Mason et al. \[2001\] Mason CR, Gomez JE, Ebner TJ (2001) Hand Synergies During Reach-to-Grasp. J Neurophysiol 86(6):2896–2910\. [10.1152/jn.2001.86.6.2896](https://ar5iv.labs.arxiv.org/doi.org/10.1152/jn.2001.86.6.2896)
- Mehring et al. \[2019\] Mehring C, Akselrod M, Bashford L, et al (2019) Augmented Manipulation Ability in Humans with Six-Fingered Hands. Nat Commun 10(1):2401\. [10.1038/s41467-019-10306-w](https://ar5iv.labs.arxiv.org/doi.org/10.1038/s41467-019-10306-w)
- Miller and Allen \[2004\] Miller A, Allen P (2004) Graspit! A Versatile Simulator for Robotic Grasping. IEEE Robot Autom Mag 11(4):110–122\. [10.1109/MRA.2004.1371616](https://ar5iv.labs.arxiv.org/doi.org/10.1109/MRA.2004.1371616)
- Moher et al. \[2009\] Moher D, Liberati A, Tetzlaff J, et al (2009) Preferred Reporting Items for Systematic Reviews and Meta-Analyses: The PRISMA Statement. Ann Intern Med 151(4):264–269\. [10.7326/0003-4819-151-4-200908180-00135](https://ar5iv.labs.arxiv.org/doi.org/10.7326/0003-4819-151-4-200908180-00135)
- Montagnani et al. \[2015\] Montagnani F, Controzzi M, Cipriani C (2015) Is it Finger or Wrist Dexterity That is Missing in Current Hand Prostheses? IEEE Trans Neural Syst Rehabil Eng 23(4):600–609\. [10.1109/TNSRE.2015.2398112](https://ar5iv.labs.arxiv.org/doi.org/10.1109/TNSRE.2015.2398112)
- Montagnani et al. \[2016\] Montagnani F, Controzzi M, Cipriani C (2016) Independent Long Fingers Are Not Essential for a Grasping Hand. Sci Rep 6(1):35545\. [10.1038/srep35545](https://ar5iv.labs.arxiv.org/doi.org/10.1038/srep35545)
- Moore and Rice \[2017\] Moore CW, Rice CL (2017) Structural and Functional Anatomy of the Palmaris Brevis: Grasping for Answers. J Anat 231(6):939–946\. [10.1111/joa.12675](https://ar5iv.labs.arxiv.org/doi.org/10.1111/joa.12675)
- Mordatch et al. \[2012\] Mordatch I, Popović Z, Todorov E (2012) Contact-Invariant Optimization for Hand Manipulation. In: ACM SIGGRAPH/Eurographics Symposium on Computer Animation (SCA). Eurographics Association, Lausanne, Switzerland, SCA ’12, pp 137–144
- Morgan et al. \[2022\] Morgan AS, Hang K, Wen B, et al (2022) Complex In-Hand Manipulation Via Compliance-Enabled Finger Gaiting and Multi-Modal Planning. IEEE Robot Autom Lett 7(2):4821–4828\. [10.1109/LRA.2022.3145961](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2022.3145961)
- Nagabandi et al. \[2020\] Nagabandi A, Konolige K, Levine S, et al (2020) Deep Dynamics Models for Learning Dexterous Manipulation. In: Conference on Robot Learning (CoRL), vol 100\. PMLR, pp 1101–1112
- Navarro-Guerrero et al. \[2017a\] Navarro-Guerrero N, Lowe R, Wermter S (2017a) The Effects on Adaptive Behaviour of Negatively Valenced Signals in Reinforcement Learning. In: Joint IEEE International Conference on Development and Learning and Epigenetic Robotics (ICDL-EpiRob), Lisbon, Portugal, pp 148–155, [10.1109/DEVLRN.2017.8329800](https://ar5iv.labs.arxiv.org/doi.org/10.1109/DEVLRN.2017.8329800)
- Navarro-Guerrero et al. \[2017b\] Navarro-Guerrero N, Lowe R, Wermter S (2017b) Improving Robot Motor Learning with Negatively Valenced Reinforcement Signals. Front Neurorobot 11(10). [10.3389/fnbot.2017.00010](https://ar5iv.labs.arxiv.org/doi.org/10.3389/fnbot.2017.00010)
- Navarro-Guerrero et al. \[2023\] Navarro-Guerrero N, Toprak S, Josifovski J, et al (2023) Visuo-Haptic Object Perception for Robots: An Overview. Auton Robots 47(4):377–403\. [10.1007/s10514-023-10091-y](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s10514-023-10091-y)
- Nelinger et al. \[2015\] Nelinger G, Assa E, Ahissar E (2015) Tactile Object Perception. Scholarpedia 10(3):32614\. [10.4249/scholarpedia.32614](https://ar5iv.labs.arxiv.org/doi.org/10.4249/scholarpedia.32614)
- Odoh et al. \[2024\] Odoh G, Landowska A, Crowe EM, et al (2024) Performance Metrics Outperform Physiological Indicators in Robotic Teleoperation Workload Assessment. Sci Rep 14(1):30984\. [10.1038/s41598-024-82112-4](https://ar5iv.labs.arxiv.org/doi.org/10.1038/s41598-024-82112-4)
- OpenAI et al. \[2019\] OpenAI, Akkaya I, Andrychowicz M, et al (2019) Solving Rubik’s Cube with a Robot Hand. [10.48550/arXiv.1910.07113](https://ar5iv.labs.arxiv.org/doi.org/10.48550/arXiv.1910.07113), [arXiv:1910.07113](https://arxiv.org/abs/1910.07113)
- Paulino et al. \[2017\] Paulino T, Ribeiro P, Neto M, et al (2017) Low-Cost 3-Axis Soft Tactile Sensors for the Human-Friendly Robot Vizzy. In: IEEE International Conference on Robotics and Automation (ICRA), pp 966–971, [10.1109/ICRA.2017.7989118](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ICRA.2017.7989118)
- Piazza et al. \[2019\] Piazza C, Grioli G, Catalano M, et al (2019) A Century of Robotic Hands. Annu Rev Control Robot Auton Syst 2(1):1–32\. [10.1146/annurev-control-060117-105003](https://ar5iv.labs.arxiv.org/doi.org/10.1146/annurev-control-060117-105003)
- Polit and Bizzi \[1979\] Polit A, Bizzi E (1979) Characteristics of Motor Programs Underlying Arm Movements in Monkeys. J Neurophysiol 42(1):183–194\. [10.1152/jn.1979.42.1.183](https://ar5iv.labs.arxiv.org/doi.org/10.1152/jn.1979.42.1.183)
- Polygerinos et al. \[2010\] Polygerinos P, Zbyszewski D, Schaeffter T, et al (2010) MRI-Compatible Fiber-Optic Force Sensors for Catheterization Procedures. IEEE Sens J 10(10):1598–1608\. [10.1109/JSEN.2010.2043732](https://ar5iv.labs.arxiv.org/doi.org/10.1109/JSEN.2010.2043732)
- Purves et al. \[2012\] Purves D, Augustine GJ, Fitzpatrick D, et al (2012) Neuroscience, 5th edn. Sinauer Associates
- Ribeiro et al. \[2020a\] Ribeiro P, Cardoso S, Bernardino A, et al (2020a) Fruit Quality Control by Surface Analysis Using a Bio-Inspired Soft Tactile Sensor. In: IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), pp 8875–8881, [10.1109/IROS45743.2020.9340955](https://ar5iv.labs.arxiv.org/doi.org/10.1109/IROS45743.2020.9340955)
- Ribeiro et al. \[2020b\] Ribeiro P, Cardoso S, Bernardino A, et al (2020b) Highly Sensitive Bio-Inspired Sensor for Fine Surface Exploration and Characterization. In: IEEE International Conference on Robotics and Automation (ICRA), Paris, France, pp 625–631, [10.1109/ICRA40945.2020.9197305](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ICRA40945.2020.9197305)
- Roa and Suárez \[2015\] Roa MA, Suárez R (2015) Grasp Quality Measures: Review and Performance. Auton Robots 38(1):65–88\. [10.1007/s10514-014-9402-3](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s10514-014-9402-3)
- Rossi et al. \[2021\] Rossi C, Bastian AJ, Therrien AS (2021) Mechanisms of Proprioceptive Realignment in Human Motor Learning. Curr Opin Physiol 20:186–197\. [10.1016/j.cophys.2021.01.011](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.cophys.2021.01.011)
- Sanchez et al. \[2018\] Sanchez J, Corrales JA, Bouzgarrou BC, et al (2018) Robotic Manipulation and Sensing of Deformable Objects in Domestic and Industrial Applications: A Survey. Int J Rob Res 37(7):688–716\. [10.1177/0278364918779698](https://ar5iv.labs.arxiv.org/doi.org/10.1177/0278364918779698)
- Santello and Soechting \[2000\] Santello M, Soechting JF (2000) Force Synergies for Multifingered Grasping. Exp Brain Res 133(4):457–467\. [10.1007/s002210000420](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s002210000420)
- Saveriano et al. \[2023\] Saveriano M, Abu-Dakka FJ, Kramberger A, et al (2023) Dynamic Movement Primitives in Robotics: A Tutorial Survey. Int J Rob Res 42(13):1133–1184\. [10.1177/02783649231201196](https://ar5iv.labs.arxiv.org/doi.org/10.1177/02783649231201196)
- Schmidt \[1975\] Schmidt RA (1975) A Schema Theory of Discrete Motor Skill Learning. Psychol Rev 82(4):225–260\. [10.1037/h0076770](https://ar5iv.labs.arxiv.org/doi.org/10.1037/h0076770)
- Schmidt and Lee \[2014\] Schmidt RA, Lee TD (2014) Motor Learning and Performance: From Principles to Application, 5th edn. Human Kinetics
- Scholz and Schöner \[1999\] Scholz JP, Schöner G (1999) The Uncontrolled Manifold Concept: Identifying Control Variables for a Functional Task. Exp Brain Res 126(3):289–306\. [10.1007/s002210050738](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s002210050738)
- Scott Kelso and Tuller \[1984\] Scott Kelso JA, Tuller B (1984) A Dynamical Basis for Action Systems. In: Handbook of Cognitive Neuroscience. Springer US, p 321–356, [10.1007/978-1-4899-2177-2\_16](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-1-4899-2177-2%5F16)
- Seminara et al. \[2013\] Seminara L, Pinna L, Valle M, et al (2013) Piezoelectric Polymer Transducer Arrays for Flexible Tactile Sensors. IEEE Sens J 13(10):4022–4029\. [10.1109/JSEN.2013.2268690](https://ar5iv.labs.arxiv.org/doi.org/10.1109/JSEN.2013.2268690)
- Senthil Kumar et al. \[2019\] Senthil Kumar K, Chen PY, Ren H (2019) A Review of Printable Flexible and Stretchable Tactile Sensors. Research 2019:1–32\. [10.34133/2019/3018568](https://ar5iv.labs.arxiv.org/doi.org/10.34133/2019/3018568)
- Siegel and Sapru \[2006\] Siegel A, Sapru HN (2006) Essential Neuroscience. Lippincott Williams & Wilkins, Philadelphia
- Slobounov et al. \[2002\] Slobounov S, Johnston J, Chiang H, et al (2002) The Role of Sub-Maximal Force Production in the Enslaving Phenomenon. Brain Res 954(2):212–219\. [10.1016/S0006-8993(02)03288-2](https://ar5iv.labs.arxiv.org/doi.org/10.1016/S0006-8993%2802%2903288-2)
- Sternad \[2000\] Sternad D (2000) Debates in Dynamics: A Dynamical Systems Perspective on Action and Perception. Hum Mov Sci 19(4):407–423\. [10.1016/S0167-9457(00)00024-5](https://ar5iv.labs.arxiv.org/doi.org/10.1016/S0167-9457%2800%2900024-5)
- Sugasawa et al. \[2021\] Sugasawa S, Webb B, Healy SD (2021) Object Manipulation Without Hands. Proc R Soc B Biol Sci 288(1947):20203184\. [10.1098/rspb.2020.3184](https://ar5iv.labs.arxiv.org/doi.org/10.1098/rspb.2020.3184)
- Sun et al. \[2022\] Sun Y, Amatova E, Chen T (2022) Multi-Object Grasping - Types and Taxonomy. In: International Conference on Robotics and Automation (ICRA), Philadelphia, PA, USA, pp 777–783, [10.1109/ICRA46639.2022.9812388](https://ar5iv.labs.arxiv.org/doi.org/10.1109/ICRA46639.2022.9812388)
- Tabot \[2013\] Tabot G (2013) Proprioception. In: Encyclopedia of Computational Neuroscience. Springer, New York, NY, USA, p 1–4, [10.1007/978-1-4614-7320-6\_381-1](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-1-4614-7320-6%5F381-1)
- Tanrıkulu et al. \[2015\] Tanrıkulu S, Bekmez Ş, Üzümcügil A, et al (2015) Anatomy and Biomechanics of the Wrist and Hand. In: Sports Injuries: Prevention, Diagnosis, Treatment and Rehabilitation, 2nd edn. Springer, Berlin, Heidelberg, p 441–447, [10.1007/978-3-642-36569-0\_49](https://ar5iv.labs.arxiv.org/doi.org/10.1007/978-3-642-36569-0%5F49)
- Tassa et al. \[2012\] Tassa Y, Erez T, Todorov E (2012) Synthesis and Stabilization of Complex Behaviors Through Online Trajectory Optimization. In: IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Vilamoura-Algarve, Portugal, pp 4906–4913, [10.1109/IROS.2012.6386025](https://ar5iv.labs.arxiv.org/doi.org/10.1109/IROS.2012.6386025)
- Taylor \[2013\] Taylor JL (2013) Kinesthetic Inputs. In: Neuroscience in the 21st Century: From Basic to Clinical, vol Sensory Systems (Neuroanatomy and Physiology). Springer New York, p 931–964
- Todorov \[2004\] Todorov E (2004) Optimality Principles in Sensorimotor Control. Nat Neurosci 7(9):907–915\. [10.1038/nn1309](https://ar5iv.labs.arxiv.org/doi.org/10.1038/nn1309)
- Todorov and Jordan \[2002\] Todorov E, Jordan MI (2002) Optimal Feedback Control as a Theory of Motor Coordination. Nat Neurosci 5(11):1226–1235\. [10.1038/nn963](https://ar5iv.labs.arxiv.org/doi.org/10.1038/nn963)
- Tomo et al. \[2016a\] Tomo TP, Somlor S, Schmitz A, et al (2016a) Design and Characterization of a Three-Axis Hall Effect-Based Soft Skin Sensor. Sensors 16(4):491\. [10.3390/s16040491](https://ar5iv.labs.arxiv.org/doi.org/10.3390/s16040491)
- Tomo et al. \[2016b\] Tomo TP, Wong WK, Schmitz A, et al (2016b) A Modular, Distributed, Soft, 3-Axis Sensor System for Robot Hands. In: IEEE-RAS International Conference on Humanoid Robots (Humanoids), pp 454–460, [10.1109/HUMANOIDS.2016.7803315](https://ar5iv.labs.arxiv.org/doi.org/10.1109/HUMANOIDS.2016.7803315)
- Tomo et al. \[2018a\] Tomo TP, Regoli M, Schmitz A, et al (2018a) A New Silicone Structure for uSkin—a Soft, Distributed, Digital 3-Axis Skin Sensor and Its Integration on the Humanoid Robot iCub. IEEE Robot Autom Lett 3(3):2584–2591\. [10.1109/LRA.2018.2812915](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2018.2812915)
- Tomo et al. \[2018b\] Tomo TP, Schmitz A, Wong WK, et al (2018b) Covering a Robot Fingertip With uSkin: A Soft Electronic Skin With Distributed 3-Axis Force Sensitive Elements for Robot Hands. IEEE Robot Autom Lett 3(1):124–131\. [10.1109/LRA.2017.2734965](https://ar5iv.labs.arxiv.org/doi.org/10.1109/LRA.2017.2734965)
- Toprak et al. \[2018\] Toprak S, Navarro-Guerrero N, Wermter S (2018) Evaluating Integration Strategies for Visuo-Haptic Object Recognition. Cognit Comput 10(3):408–425\. [10.1007/s12559-017-9536-7](https://ar5iv.labs.arxiv.org/doi.org/10.1007/s12559-017-9536-7)
- Wade et al. \[2017\] Wade J, Bhattacharjee T, Williams RD, et al (2017) A Force and Thermal Sensing Skin for Robots in Human Environments. Rob Auton Syst 96:1–14\. [10.1016/j.robot.2017.06.008](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.robot.2017.06.008)
- Wadman et al. \[1979\] Wadman W, Denier J, Geuze R, et al (1979) Control of Fast Goal-Directed Arm Movements. J Hum Movement Stud 5(1):3–17
- Wang et al. \[2008\] Wang X, Baron L, Cloutier G (2008) Topology of Serial and Parallel Manipulators and Topological Diagrams. Mech Mach Theory 43(6):754–770\. [10.1016/j.mechmachtheory.2007.05.005](https://ar5iv.labs.arxiv.org/doi.org/10.1016/j.mechmachtheory.2007.05.005)
- Wang et al. \[2018\] Wang YC, Bohannon RW, Li X, et al (2018) Hand-Grip Strength: Normative Reference Values and Equations for Individuals 18 to 85 Years of Age Residing in the United States. J Orthop Sports Phys Ther 48(9):685–693\. [10.2519/jospt.2018.7851](https://ar5iv.labs.arxiv.org/doi.org/10.2519/jospt.2018.7851)
- Ward-Cherrier et al. \[2018\] Ward-Cherrier B, Pestell N, Cramphorn L, et al (2018) The TacTip Family: Soft Optical Tactile Sensors with 3D-Printed Biomimetic Morphologies. Soft Robot 5(2):216–227\. [10.1089/soro.2017.0052](https://ar5iv.labs.arxiv.org/doi.org/10.1089/soro.2017.0052)
- Wells and Greig \[2001\] Wells R, Greig M (2001) Characterizing Human Hand Prehensile Strength by Force and Moment Wrench. Ergonomics 44(15):1392–1402\. [10.1080/00140130110109702](https://ar5iv.labs.arxiv.org/doi.org/10.1080/00140130110109702)
- Wolpert and Flanagan \[2001\] Wolpert DM, Flanagan JR (2001) Motor Prediction. Curr Biol 11(18):R729–R732\. [10.1016/S0960-9822(01)00432-8](https://ar5iv.labs.arxiv.org/doi.org/10.1016/S0960-9822%2801%2900432-8)
- Wolpert and Ghahramani \[2000\] Wolpert DM, Ghahramani Z (2000) Computational Principles of Movement Neuroscience. Nat Neurosci 3(11):1212–1217\. [10.1038/81497](https://ar5iv.labs.arxiv.org/doi.org/10.1038/81497)
- Wolpert et al. \[2011\] Wolpert DM, Diedrichsen J, Flanagan JR (2011) Principles of Sensorimotor Learning. Nat Rev Neurosci 12(12):739–751\. [10.1038/nrn3112](https://ar5iv.labs.arxiv.org/doi.org/10.1038/nrn3112)
- Xia et al. \[2022\] Xia Z, Deng Z, Fang B, et al (2022) A Review on Sensory Perception for Dexterous Robotic Manipulation. Int J Adv Robot Syst 19(2):17298806221095974\. [10.1177/17298806221095974](https://ar5iv.labs.arxiv.org/doi.org/10.1177/17298806221095974)
- Young et al. \[2013\] Young KA, Wise JA, DeSaix P, et al (2013) Anatomy & Physiology. XanEdu Publishing Inc.
- Yuan et al. \[2017\] Yuan W, Dong S, Adelson EH (2017) GelSight: High-Resolution Robot Tactile Sensors for Estimating Geometry and Force. Sensors 17(12):2762\. [10.3390/s17122762](https://ar5iv.labs.arxiv.org/doi.org/10.3390/s17122762)
- Zakka et al. \[2023\] Zakka K, Wu P, Smith L, et al (2023) RoboPianist: Dexterous Piano Playing with Deep Reinforcement Learning. In: Conference on Robot Learning (CoRL), vol 229\. PMLR, pp 2975–2994
- Zhu et al. \[2021\] Zhu T, Wu R, Lin X, et al (2021) Toward Human-Like Grasp: Dexterous Grasping via Semantic Representation of Object-Hand. In: IEEE/CVF International Conference on Computer Vision (ICCV), Virtual, pp 15741–15751
- Zitkovich et al. \[2023\] Zitkovich B, Yu T, Xu S, et al (2023) RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic Control. In: Conference on Robot Learning (CoRL), vol 229\. PMLR, pp 2165–2183

\\bmhead

Publisher’s Note Springer Nature remains neutral with regard to jurisdictional claims in published maps and institutional affiliations.