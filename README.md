Report:


Image Colorization Internship Project


Intern: Sumit Gupta

Project: Learn to Build a Real-Time GenAI Image Colorization (v2)

GitHub Repository: https://github.com/Sumit-081002/Internship-Data-Science
Live URL: https://f212031a86aebb7bd0.gradio.live


Overview:
This project delivers a complete image colorization suite covering all six internship tasks, built upon an Educational Stable Diffusion Text-to-Image Generator architecture. The foundational pipeline incorporates a robust multi-checkpoint resolver with automatic fallback across verified Stable Diffusion checkpoints and dedicated pipeline handling for SDXL (RealVisXL) alongside standard SD 1.x models. Each task is implemented as a dedicated tab within a unified Gradio application, creating a cohesive, production-ready system rather than separate experiments.  Technical Approach by Task

Task 1 — Real-Time Multi-Object Colorization with Semantic Segmentation 
Implements GPU-accelerated semantic segmentation integrated into a continuous video processing loop. The model processes every video frame without skipping to satisfy real-time constraints, assigning consistent color classes across detected objects (such as buildings, sky, and vegetation). The Gradio interface supports both live webcam streaming and video file upload.  

Task 2 — Conditional Image Colorization 
Combines semantic segmentation with pixel-level color control. The detected segmentation masks are converted into LAB color space: the chromatic channels ($a^*$ and $b^*$) are recolored based on user-designated region specifications, while the original lightness ($L^*$) channel is preserved intact. This ensures exact boundary adherence and prevents color bleeding while maintaining natural shading and texture.  

Task 3 — Context-Aware Colorization of Complex Scenes 
Extends region-based recoloring by integrating scene-geometry heuristics computed directly over the segmentation mask. The engine incorporates a reflection heuristic to tint reflective surfaces (e.g., water, glass, mirrors) situated below sky or architectural elements, alongside a shadow heuristic that desaturates and cools the darkest luminance regions to model ambient lighting realistically.  

Task 4 — Time-Based Historical 
Image Colorization Employs a CLIP-based zero-shot classification model to identify the historical era of input photographs. The system pairs detected eras with deterministic color-grading curves (calibrating sepia, tint, and saturation values per period) to ensure faithful historical tones, which can operate independently or alongside generative diffusion refinement.  

Task 5 — Cross-Domain Image Colorization 
Implements domain-specific processing pipelines tailored to distinct visual modalities. Artistic sketches and standard grayscale photos are processed using generative diffusion img2img, satellite imagery utilizes deterministic band-remapping, and medical/X-ray inputs are routed exclusively through deterministic intensity colormaps to prevent generative hallucinations on diagnostic images.  

Task 6 — Colorization of Historical Photographs
Utilizes a dedicated, lightweight U-Net architecture trained specifically for end-to-end grayscale-to-color mapping. The model is trained for 15 epochs on locally generated paired grayscale/color datasets using an automated desaturation pipeline. The resulting model weights are stored locally in the project repository to deliver structured, historically consistent colorization on unseen monochrome photography.  

Tools & Libraries: 
Stable Diffusion v1.5 / RealVisXL (diffusers), SegFormer / CLIP (transformers), PyTorch (U-Net training and inference), OpenCV, Gradio, and Google Colab (GPU execution).  

Limitations:
Generative diffusion img2img paths can occasionally alter fine structural details at higher denoising strengths, requiring balanced strength parameters to preserve facial features.  The Task 6 U-Net model was trained on a compact paired dataset; scaling the dataset volume would further generalize color reconstruction across diverse eras.  Real-time video colorization (Task 1) prioritizes low-latency throughput via class-based color masks to maintain continuous frame rates, rather than running multi-step diffusion passes per frame.  

Conclusion:
All six colorization tasks were successfully engineered, integrated into a unified multi-tab Gradio application, and verified across diverse real-world benchmarks. The system provides a stable, modular framework combining generative diffusion, custom neural network training, and deterministic computer vision algorithms.
