# Bulking-Cutting-App
Research on a Portable AI Coaching System for Fat Loss and Muscle Gain
Liangheng Wang
(International Division, Affiliated High School of Shandong Normal University, Jinan 250014, China)
Abstract:
To address the scarcity of professional coaching resources and the challenge of deploying general-purpose Transformer-based large language models (LLMs) on mobile devices due to their high computational demands, this study proposes a portable AI coaching system tailored for fat loss and muscle gain. The system comprises an edge computing platform and a wearable data acquisition terminal. It leverages a quantized version of the gpt-oss-20b foundation model and the lightweight MediaPipe-Pose-Estimation motion recognition model, both optimized for on-device execution. Upon inputting baseline biometric data (e.g., age, sex, height, weight), the system computes key physiological metrics—including Body Mass Index (BMI), Basal Metabolic Rate (BMR), and Total Daily Energy Expenditure (TDEE)—to generate personalized training and nutrition plans. During workouts, it performs real-time pose estimation to assess exercise form, provides corrective feedback, and synchronously monitors vital signs such as heart rate via Bluetooth-connected smartwatches or fitness bands. Post-exercise, the system compiles a comprehensive evaluation report. Experimental results demonstrate that the system operates independently of network connectivity, significantly reduces reliance on human coaches, and is adaptable to both elite athletic training and general public fitness contexts. This work holds practical significance for advancing scientific training methodologies and promoting inclusive physical wellness.
Keywords: fat loss and muscle gain; AI coach; Transformer large model; edge computing; pose estimation; biometric monitoring

1. Introduction
In modern competitive sports, optimizing an athlete’s physical condition is central to enhancing performance, minimizing injury risk, and extending athletic longevity. Fat loss coupled with muscle gain—far beyond mere aesthetic goals—serves as a critical strategy in this optimization process. However, access to qualified coaching remains limited, particularly for grassroots athletes and recreational fitness enthusiasts, who often resort to unguided training regimens that compromise efficacy and safety.
Recent advances in artificial intelligence (AI), especially the emergence of Transformer-based large models, offer promising avenues to mitigate this gap. Such models can complement human expertise by generating personalized programs, delivering real-time biomechanical feedback, and interpreting complex physiological data streams. Nevertheless, their deployment in mobile or field settings is hindered by substantial hardware constraints: contemporary LLMs typically require tens of gigabytes of memory and high-bandwidth compute infrastructure, which are unavailable on consumer-grade smartphones or wearables.
To overcome these limitations, we present a portable AI coaching system that integrates domain-specific knowledge from sports science with efficient AI architectures. By applying model quantization and pruning techniques, we enable local execution of a 20-billion-parameter language model (gpt-oss-20b) alongside a lightweight pose estimation module (MediaPipe-Pose) on standard mobile devices. This “coach-in-your-pocket” approach enhances training accessibility, scientific rigor, and user autonomy—bridging the divide between elite sports science and public health promotion.
2. AI-Driven Approaches to Fat Loss and Muscle Gain
2.1 Significance in Athletic Performance
For athletes, fat loss and muscle gain are not merely cosmetic pursuits but strategic interventions that directly influence competitive outcomes:

    Enhanced Sport-Specific Performance: Reducing non-functional adipose tissue while increasing functional lean mass improves power-to-weight ratios—critical in explosive disciplines like sprinting and jumping. It also bolsters muscular endurance for endurance sports (e.g., long-distance running, swimming) and refines neuromuscular control for precision-demanding activities (e.g., gymnastics, shooting).
    Injury Risk Mitigation: Greater muscle mass strengthens joint stabilization and shock absorption, lowering the incidence of osteoarthritis and ligamentous injuries. Balanced musculature also corrects biomechanical asymmetries that predispose athletes to overuse injuries.
    Metabolic and Hormonal Optimization: Skeletal muscle is a primary site of energy metabolism; increased muscle mass elevates resting metabolic rate and accelerates post-exercise recovery. Moreover, structured resistance training stimulates anabolic hormone secretion (e.g., testosterone), supporting sustained peak performance.
    Weight-Class Compliance: In sports with weight categories (e.g., boxing, weightlifting), precise body composition management enables athletes to compete at optimal weight classes without compromising strength or health.

Thus, fat loss and muscle gain constitute a performance-centered physiological optimization strategy embedded within evidence-based training paradigms [2].
2.2 Applications and Limitations of Large Models in Sports
2.2.1 Potential Contributions
Transformer-based LLMs can augment coaching through:

    Personalized Program Design: Integrating user profiles (age, training history, goals) to produce periodized plans (e.g., combining endurance, strength, and recovery phases for marathoners).
    Real-Time Form Correction: Using video analysis to detect deviations (e.g., knee valgus during squats) and provide visual/verbal cues for correction.
    Multimodal Data Synthesis: Interpreting heart rate variability, step cadence, and movement kinematics to assess fatigue and adjust intensity dynamically [3].

2.2.2 Deployment Challenges
Despite their capabilities, general-purpose LLMs face four key barriers to mobile deployment:

    Memory and Storage Constraints: Models with billions of parameters demand tens of GBs of RAM and storage—exceeding typical smartphone capacities.
    Insufficient Compute Throughput: Mobile CPUs/GPUs lack the parallel processing power of cloud servers, leading to unacceptable latency.
    Memory Bandwidth Bottlenecks: Frequent weight accesses strain limited memory bandwidth, slowing inference.
    Absence of Dedicated AI Accelerators: Most consumer devices lack NPUs or TPUs optimized for Transformer operations, further degrading efficiency.

To resolve these issues, we adopt model compression techniques (quantization, pruning) to retain domain-relevant biomedical knowledge while enabling on-device operation on widely available hardware (smartphones and wearables).
3. System Architecture
3.1 Problem Statement
Traditional training relies heavily on human coaches for program design and form correction—a model unsustainable given global coaching shortages. Our system democratizes access by embedding expert knowledge into a portable, offline-capable AI assistant usable anywhere: gyms, homes, or outdoor fields.
3.2 System Design
The system consists of two wirelessly connected components:
3.2.1 Edge Computing Platform

    Hardware: Smartphone with ≥2.3 GHz CPU and ≥16 GB RAM.
    OS: iOS or Android (ensuring broad compatibility).
    Core Models:
        gpt-oss-20b (quantized): Computes BMI, BMR, TDEE; generates personalized nutrition and workout plans.
        MediaPipe-Pose-Estimation: Lightweight CNN-based model for real-time 2D/3D pose tracking (≈3 MB).
    Model Management: Implemented via PocketAI-by-LangGPT v1.6.9.apk, allowing dynamic model switching based on task phase (planning vs. execution).

3.2.2 Data Acquisition Terminal

    Device: Commercial smartwatch or fitness band.
    Sensors: Optical heart rate monitor, accelerometer, gyroscope.
    Function: Continuously records heart rate, steps, and activity duration; transmits data via Bluetooth to the smartphone for real-time analytics and post-session reporting.

3.2.3 Auxiliary Hardware

    Smartphone Mount: Ensures stable, full-body video capture for accurate pose estimation.

3.3 Key Advantages

    Network Independence: All models run locally; Bluetooth communication requires no internet.
    Minimal User Interference: Wearables are ergonomically designed to avoid disrupting movement.
    Environmental Flexibility: Operates in any setting—urban parks, home gyms, remote areas.
    Reduced Coaching Dependency: Delivers end-to-end guidance (planning → execution → evaluation), particularly beneficial in underserved regions.

4. System Workflow
4.1 Planning Phase

    User installs PocketAI and loads the quantized gpt-oss-20b model.
    Inputs biometrics (sex, age, height, weight).
    System calculates:
        BMI: Assesses adiposity and health risk.
        BMR: Estimates caloric needs at rest.
        TDEE: Projects total daily energy expenditure.
    Generates a holistic plan specifying nutrition guidelines, exercise types, intensity, frequency, and duration.
    Unloads gpt-oss-20b and loads MediaPipe-Pose for real-time analysis.

4.2 Execution Phase

    Smartphone is mounted; wearable pairs via Bluetooth.
    During exercise, MediaPipe analyzes live video feed:
        Detects form errors (e.g., excessive forward knee translation in squats).
        Provides immediate visual/auditory feedback with corrective demonstrations.
    Wearable streams physiological data (e.g., heart rate) to the phone for concurrent workload assessment.

4.3 Evaluation Phase

    Post-workout, the system compiles a report including:
        Exercise completion rate.
        Pose accuracy scores (per movement).
        Temporal trends in biometric markers.
    Data is visualized as interactive charts to inform future adjustments.
    Feedback loop refines subsequent training prescriptions for adaptive personalization.

5. Conclusion and Future Work
This study successfully integrates sports science expertise with efficient AI engineering to deliver a portable, offline-capable coaching system for fat loss and muscle gain. By overcoming the deployment barriers of large models through quantization and leveraging ubiquitous mobile/wearable hardware, our solution enhances training accessibility, safety, and efficacy across both elite and recreational contexts.
Future directions include:

    Model Refinement: Further compression via knowledge distillation; integration of reinforcement learning for adaptive planning.
    Hardware Expansion: Incorporation of smart footwear or EMG-enabled garments to capture ground reaction forces and muscle activation patterns.
    Clinical Extension: Adaptation for post-injury rehabilitation protocols under medical supervision.

As edge AI and wearable sensing technologies mature, such systems will play an increasingly vital role in personalized health and performance optimization.
References
[1] Zhao, Y., & Chen, L. (2024). Artificial Intelligence in Competitive Sports: Current Status and Prospects. Contemporary Sports Technology, 25, 175–178.
[2] Chen, L. (2024, October 25). The Scientific Relationship Between Muscle Gain and Fat Loss. Public Health Newspaper.
[3] CaiTong Securities. (2025). 2025 Special Report on AI Large Models: The Past, Present, and Future of Transformer Architectures. Retrieved from https://www.vzkoo.com/read/20250120982a8eb84de49552c13277a7.html
[4] OpenAI. (2025). gpt-oss-20b Documentation. Hugging Face. https://huggingface.co/openai/gpt-oss-20b
[5] Google. (2025). MediaPipe Pose Estimation Documentation. GitHub. https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/pose.md
[6] Wang, L., Wu, C., & Fan, W. (2021). A Survey on Resource Allocation and Task Scheduling Optimization in Edge Computing. Journal of System Simulation, 33(3), 509–520.
[7] Jin, S. (2025). Applications and Trends of Smart Wearables in Sports Monitoring. Sports Equipment & Science & Technology, 11, 190–192.
[8] Jiang, Q. (2024). Applications and Impacts of Intelligent Sports in Promoting National Fitness. Sports Equipment & Science & Technology, 3, 187–189.
