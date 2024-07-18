# Project 0 Getting Started: Instructions

This is due **August 30 2024**. (See [late policy](#late-policy) at the bottom)

**Summary:** In this project, you will set up your GPU development tools and verify that you can build, run, and do performance analysis.

This project contains:

1. **CUDA**: A simple program that demonstrates CUDA and OpenGL functionality and interoperability, testing that CUDA has been properly installed. If the machine you are working on has CUDA and OpenGL 4.0 support, then when you run the program, you should see either one or two colors depending on your graphics card.
2. **WebGL**: A guide to enable WebGL support on your machine.
3. **WebGPU**: A guide to choose a browser that supports WebGPU

**If your machine fails any of these (CUDA, WebGL), use the CETS Virtual Lab or SIGLAB's computers for your development. Your submission will require certain screenshots.**

## Part 1: Setup your Development Environment

CIS 5650 projects require a compatible NVIDIA GPU. As some of you may not have an NVIDIA GPU in your personal computers, we have made them available through the CETS Virtual Lab.

Follow the [Hardware and Software Setup](https://cis5650-fall-2024.github.io/setup/) pages on the course website to set up your development environment.

*Notes:*

* Before you get started: if you have multiple Visual Studio and/or CMake versions, you will probably run into trouble. Either uninstall extra versions (if possible) or ensure that the correct Visual Studio and CMake versions are being chosen.
* If you are running into a lot of trouble, a clean installation of Visual Studio 2022, CMake, and CUDA can help fix any problems if other methods don't work.
* If you have driver issues or random crashing: uninstalling and reinstalling drivers usually works

### Setup you Git Environment

0. You will need Git installed. Some computers including CETS Virtual Lab may have Git installed. To check if Git is installed, open Command Prompt/Git Bash/Terminal and run `git`. To install Git:
    * **Windows:** [Git](https://git-scm.com/download/win)
    * **Linux:** `apt install git` on Debian/Ubuntu
1. If you haven't used Git, you'll need to set up a few things.
    * On Windows: In order to use Git commands, you can use Git Bash. You can right-click in a folder and open Git Bash there.
    * On Linux: Open a terminal.
    * Configure git with some basic options by running these commands:
        * `git config --global push.default simple`
        * `git config --global user.name "YOUR NAME"`
        * `git config --global user.email "GITHUB_USER@users.noreply.github.com"`
        * (Or, you can use your own address, but remember that it will be public!)
2. Clone from GitHub onto your machine:
    * Navigate to the directory where you want to keep your 5650 projects, then
     clone your fork.
        * `git clone` the clone URL from your GitHub fork homepage.

Note: Do not clone projects directly from the [CIS5650-Fall-2024](https://github.com/CIS5650-Fall-2024) GitHub organization. Be sure to fork the project on GitHub first to your own account and then clone it using your fork.

*Getting Started with GitHub Resources:*

* [How to use GitHub](https://guides.github.com/activities/hello-world/)
* [How to use Git](http://git-scm.com/docs/gittutorial)

## Part 3: Project Instructions

### Part 3.1: CUDA

Build and run the project and follow the instructions below to complete your README.

In your README, report the Compute Capability of your CUDA-compatible GPU (sometimes called `sm`). Here is the [list of CUDA-compatible GPUs](https://developer.nvidia.com/cuda-gpus) along with their Compute Capabilities.

* `cuda-getting-started/src/` contains the source code.
* `cuda-getting-started/external/` contains the Windows binaries and headers for GLEW and GLFW.

**CMake note:** Do not change any build settings or add any files to your project directly (in Visual Studio, Nsight, etc.) Instead, edit the `cuda-getting-started/src/CMakeLists.txt` file. Any files you add must be added here. If you edit it, just rebuild your VS/Nsight project to make it update itself.

#### Windows

1. In Git Bash, navigate to your cloned project directory.
2. Create a `build` directory: `mkdir build`
    * (This "out-of-source" build makes it easy to delete the `build` directory and try again if something goes wrong with the configuration.)
3. Navigate into that directory: `cd build`
4. Open the CMake GUI to configure the project:
    * `cmake-gui ..` or `"C:\Program Files (x86)\cmake\bin\cmake-gui.exe" ..`
        * Don't forget the `..` part! This tells CMake that the `CMakeLists.txt` file is in the parent directory of `build`.
    * Make sure that the "Source" directory points to the directory `cuda-getting-started`.
    * Click *Configure*.
        * Select your Visual Studio version (2019 or 2017), and `x64` for your platform. (**NOTE:** you must use x64, as we don't provide libraries for Win32.)
    * Click *Generate*.
5. If generation was successful, there should now be a Visual Studio solution (`.sln`) file in the `build` directory that you just created. Open this with Visual Studio.
6. Build. (Note that there are Debug and Release configuration options.)
7. Run. Make sure you run the `cis5650_` target (not `ALL_BUILD`) by right-clicking it and selecting "Set as StartUp Project".
    * If you have switchable graphics (NVIDIA Optimus), you may need to force your program to run with only the NVIDIA card. In NVIDIA Control Panel, under "Manage 3D Settings," set "Multi-display/Mixed GPU acceleration" to "Single display performance mode".

#### Linux

It is recommended that you use Nsight. Nsight is shipped with CUDA. If you set up the environment path correctly `export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}` (Note that simply typing the `export` command is a temporary change. The `PATH` variable won't be updated permanently. For permanent change, add it to your shell configuration file, e.g. `~/.profile` on Ubuntu), you can run Nsight by typing `nsight` in your terminal.

1. Open Nsight. Set the workspace to the one *containing* your cloned repo.
2. *File->Import...->General->Existing Projects Into Workspace*.
    * Select the `cuda-getting-started` directory as the *root directory*.
3. Select the *cis5650-* project in the Project Explorer. Right click the project. Select *Build Project*.
    * For later use, note that you can select various Debug and Release build configurations under *Project->Build Configurations->Set Active...*.
4. If you see an error like `CUDA_SDK_ROOT_DIR-NOTFOUND`:
    * In a terminal, navigate to the build directory, then run: `cmake-gui ..`
    * Set `CUDA_SDK_ROOT_DIR` to your CUDA install path.  This will be something like: `/usr/local/cuda`
    * Click *Configure*, then *Generate*.
5. Right click and *Refresh* the project.
6. From the *Run* menu, *Run*. Select "Local C/C++ Application" and the `cis5650_` binary.

### Part 3.1.1: Modify the CUDA Project and Take a Screenshot

1. Search the code for `TODO`: you'll find one in `cuda-getting-started/src/main.cpp` on line 13. Change the string to your name, rebuild, and run. (`m_yourName = "TODO: YOUR NAME HERE";`)
2. Take a screenshot of the window (including title bar) and save it to the `images` directory for Part 4.
3. You're done with some code changes now; make a commit!
    * Make sure to `git add` the `main.cpp` file.
    * Use `git status` to make sure you didn't miss anything.
    * Use `git commit` to save a version of your code including your changes.Write a short message describing your changes.
    * Use `git push` to sync your code history to the GitHub server.

### Part 3.1.2: Analyze

#### Windows

1. Go to the Nsight menu in Visual Studio.
    * If you dont see the Nsight Menu in the top panel then it's located inside the Extensions Menu, considering you have setup your environment correctly.*
    * *Enable `Nsight` menu to appear in the top Navigation panel instead of the Extensions Menu*
        * Click the `Extensions` button located at the top Panel
        * Click on `Customize Menu..` button located in the 'Extensions' drop down menu. This will open up the Customise Dialog Box.
        * Un-check `Nsight Developer Tools Inegration` and `Nsight Visual Studio Edition` located in the Extensions Menu of the Customise Dialog Box.
        * Restart Visual Studio.
2. Click on *Nsight Systems _Your Version of Nsight_*.
3. Select *Trace*.
4. Click *Target for profiling...*. Select your machine under 'Localhost connection'.
5. Under *Trace Settings* that now appear, enable tracing for CUDA and OpenGL.
6. Click *Start*.
    * If you have switchable graphics (NVIDIA Optimus), see the note in Part 3.1.
7. Run the program for a few seconds, then close it.
8. At the top of the report page, select *Timeline* from the drop-down menu.
9. Take a screenshot of this tab and save it to `images`, for Part 4.

#### Linux

1. Open your project in Nsight.
2. *Run*->*Profile*.
3. Run the program for a few seconds, then close it.
4. Take a screenshot of the timeline and save it to `images`, for Part 4.

### Part 3.1.3: Nsight Debugging

#### Windows

1. Switch your build configuration to "Debug" and `Rebuild` the solution.
2. Select the Nsight menu in Visual Studio and select *Start CUDA Debugging (Next-Gen)*.
    * If you have an older GPU, like GTX 9xx or older, then you may have to use *Start CUDA Debugging (Legacy)*.
3. If prompted, select the *Connect Unsecurely* option to start Nsight.
4. Exit the app.
5. Now place a breakpoint at Line 79 of `kernel.cu` => `if (x <= width && y <= height) {`
6. Restart the CUDA Debugging. This time, the breakpoint should be hit.
    * The *Autos* and *Locals* debugging tabs should appear at the bottom. (You can also open this from Debug -> Windows -> Autos/Locals)
    * Notice the values that are in the autos.
7. The following steps should be done with Nsight CUDA Debugging running.
8. Go to Nsight menu and select *Next Active Warp*. Now notice the values that have changed (highlighted in red).
9. Now, let's try to go to a particular index (pick your own number - anything greater than 1000).
    * Right click the breakpoint and select conditions.
    * The window that pops up should have defaults *Conditional Expression* and *is true*.
    * In the third box, put it `index == <your number>`.
    * Click close.
10. Now click *Continue* in the Visual Studio toolbar.
11. The breakpoint should be hit one more time. This time, the Autos window will should `index` as your number.
12. Goto  `Nsight` -> `Windows` -> `Warp Info`(if using older versions of Nsight, go to `Nsight` -> `Windows` -> `CUDA Info` -> `CUDA Info 1`).
    * This window shows information about the kernel, threads, blocks, warps, memory allocations etc. Choose from the drop downs to view each.
    * If using older version of Nsight, you may need to select *Warp* and keep it that way.
13. Find the yellow arrow by mapping `blockIdx` and `threadIdx` in `Autos` -> to `CTA` and `Thread` respectively under the `Shader Info` column. Click on the row to highlight it. Take a screenshot of this *Autos* window and the *Warp Info* as a image and save it under `images`.
    * Optionally, you may choose to double click on any one of the boxes in the "Threads" grid and watch the *Autos* window update the value.
14. Play around with Nsight debugger as much as you want.

#### Linux

1. Create a directory called `eclipse` under `Project0-Getting-Started`. `eclipse` should be a sibling directory to `cuda-getting-started`. (The name `eclipse` itself is not important, but that's the example here)
2. CD into the `eclipse` directory, then run the command
    ```
    cmake ../cuda-getting-started -G "Eclipse CDT4 - Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug
    ```
    * Note: Change `Debug` to `Release` when running the profiler.
3. Open Nsight Eclipse Edition
4. Select File -> Import.
5. Then in the pop up box, select `General -> Existing Project into Workspace".
6. In `Select Root Directory` browse to the `eclipse` directory.
7. This will populate the box below with `cis5650_getting_started.....`.
8. Select this and click "Finish".

Now you can carry on running the executable and other profiler and debug steps.

### Part 3.2: WebGL

1. Download [Google Chrome](https://www.google.com/chrome/) if not already installed
2. Check that you have [WebGL support](https://webglreport.com)
3. If step 2 doesn't show WebGL compatibility, then try the following:
    * *Enabling WebGL*
        * Go to `chrome://settings` (in the address bar)
        * Click the `Advanced` button at the bottom of the page
        * In the `System` section, ensure the `Use hardware acceleration when available` checkbox is checked (you'll need to relaunch Chrome for any changes to take effect)
        * Go to `chrome://flags`
        * Ensure that `Disable WebGL` is not activated (you'll need to relaunch Chrome for any changes to take effect)
            * In newer versions, this option of `Disable WebGL` will not be available, you will instead have to search for `WebGL 2.0` (or some different version)
            * If an option appears as `Default`, changed it to `Enabled`
            * You should also change `Override software rendering list` to `Enabled`
    * *Checking WebGL status*
        * Go to `chrome://gpu`
        * Inspect the WebGL item in the Graphics Feature Status list. The status will be one of the following:
            * Hardware accelerated - WebGL is *enabled* and hardware-accelerated (running on the graphics card).
            * Software only, hardware acceleration unavailable - WebGL is *enabled*, but running in software.
            * Unavailable - WebGL is *not available* in hardware or software.

**Take a screenshot** the output of `https://webglreport.com` or `chrome:\\gpu` and save it to `\images`. Your submission must show that WebGL works on your machine (or any machine you plan to develop on, e.g: Moore or SIGLAB machines).

### Part 3.3: WebGPU

1. Download [Google Chrome](https://www.google.com/chrome/) if not already installed
    * See a list of supported browsers and versions at https://github.com/gpuweb/gpuweb/wiki/Implementation-Status.
2. Check that you have [WebGPU support](https://webgpureport.org/)
    * If you have multiple GPUs on your computer (eg. Intel and NVIDIA), then look at the `Adapter Info`. Use your device settings to change the GPU and then refresh the page to see if the GPU has updated.
3. If step 2 doesn't show WebGPU compatibility, then follow the instruction in https://developer.chrome.com/docs/web-platform/webgpu/troubleshooting-tips.

**Take a screenshot** the output of https://webgpureport.org or any one of https://webgpu.github.io/webgpu-samples/ and save it to `\images`. Your submission must show that WebGPU works on your machine (or any machine you plan to develop on, e.g: Moore or SIGLAB machines).

## Part 4: Write-up

1. Update ALL of the TODOs at the top of this README:
    * Finish your `README.md`
    * Add your name, computer, and whether it's a personal or lab computer.
    * Embed the screenshots you took: `![](images/example.png)`
    * Syntax help: https://help.github.com/articles/writing-on-github/
2. Add, commit, and push your screenshots and README.
    * Make sure your README looks good on GitHub!
3. If you have modified either of the `CMakeLists.txt` at all (aside from the list of `SOURCE_FILES`), mention it explicitly.

## Submit

If you are using a private fork and do not want to make a public pull request, contact the staff to submit. You still must submit before the due date.

Open a GitHub pull request so that we can see that you have finished.
The title should be "Project 0: YOUR NAME".
The template of the comment section of your pull request is attached below, you can do some copy and paste:

* [Repo Link](https://link-to-your-repo)
* (Briefly) Mentions features that you've completed. Especially those bells and whistles you want to highlight
    * Feature 0
    * Feature 1
    * ...
* Feedback on the project itself, if any.

And you're done!

## Late-Policy

* Due at midnight on the due date
* Submitted using GitHub
* Late Policy
    * Up to 1 week late:  50% deduction
    * Use up to 4 bonus days over the semester to extend the due date without penalty
    * Examples
        * Extend 4 projects by 1 day each
        * OR: Extend 1 project by 4 days
        * OR: Extend 2 projects by 2 days each
* Can't be used for the final project
