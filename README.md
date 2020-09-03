# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Sumamry

This is a simple C++ implementation of a simple PID controller.

### Hyperparameters

The PID controller in this project is used to control steering angle based on cross track error (CTE).
However general principle can be used for any control correction (e.g. speed).

It consists of 3 hyperparameters that have differenet relation to CTE used in 3 terms. Terms of the PID controller are explained below:

- **Proportional** hyperparameter is mutliplied with CTE which result in sharp angles if CTE is high and gentle is CTE is low.
  It is responsible of getting the vehicle close to the target path. Without other parameters contoller would just oscillate around
  reference position and wold not be able to reach it.

- **Integral** hyperparameter is multiplied with sum of CTEs over time period.
  This would smooth the errors caused by biased errors (e.g. steeering drift).

- **Derivative** hyperparameter is multiplied with delta CTE. Delta CTE is represented as difference between current nad previous CTE.

Final angle is calculated as a negative sum of these 3 products.

### Parameter tuning

There are various methods to tune these parameters Twiddle, SGD, Trial and Error Method and etc. I used manual tuning with Trial and Error Method.

- Start with setting derivative and integral to zero, and only tune proportional term.
  Until vehicle has stable oscilating around center of the lane which is reference position tweek the this parameter.

- Next step is to wweek derivative term to try and smooth out the oscilations of the vehicle. This means fixing overshooting of the reference position.

- As integral part is used to fix the biases and in the simulation there are none, this parameter is very small.
  In this concrete project it could be even suppresed by setting it's value to 0.

Final parameters that drove a vehicle in the lane boundaries with decent steering are [P: 0,195, I: 0.0002, D: 2.9].

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.
