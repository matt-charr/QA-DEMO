[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

<br />
<p align="center">
  <a href="https://github.com/matt-charr/QA-DEMO">
    <img src="https://github.com/matt-charr/QA-DEMO/blob/main/ribbon.jpg" alt="Logo" width="400" height="300">
  </a>

  <h3 align="center"><strong>QA</strong></h3>

  <p align="center">
    <em>Quantitative Analytics</em>
  </p>
</p>

<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#genesis">Genesis</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#access">Access</a></li>
        <li><a href="#installation">Installation</a></li>
        <li><a href="#compilation">Compilation</a></li>
      </ul>
    <li><a href="#tools">Tools</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

## Genesis

This repository aims at efficiently design a cutting-edge technology for market finance industry which, as discovering interesting theoretical concepts closely studied from masterbooks, will be fortified.

Feel free to concat the author should you desire any of the tools below integrated within your own library.

## Getting Started

### Access

The repository **CORE** is located on GitHub with a restricted access.

In case you wish to contribute and share interesting addons of functionality, please kindly contact the owner to explain your addins. 

Subject to approval, a fixed time limited access will be granted.

### Installation

Once you received your access, you simply need to clone this repository to your machine:

  ```sh
  mkdir myQA
  cd myQA
  git clone https://github.com/matt-charr/QA.git
  ```

### Compilation

To compile the project, it is necessary to have CMake installed on your machine.
It is recommended to make a *bin* directory to store the executables and a *build* directory to store the makefiles.

  ```sh
  cd myQA
  mkdir build bin
  cd build/
  cmake -G "MinGW Makefiles" ..
  make .
  ```

And:

```sh
  ../bin/test_*.cpp
  ```

to execute.

## Tools

The project contains several functionnalities. Please find below a non exhaustive list:

* **MARKET DATA IMPORTER**

You can import market data from a market data file you can create and drop in *data/internal/*. This file must contains lines of observables such as:

<img src="https://github.com/matt-charr/QA-DEMO/blob/main/market_data.png" alt="MarketData" width="400" height="300">


* **CONTRACT ALGEBRA**

* **MONTE CARLO INSPECTOR**

* **PARTIAL DIFFERENTIAL EQUATION INSPECTOR**

* **STATIC REPLICATION INSPECTOR**

* **BLACK SCHOLES MODEL**

* **MULTI BLACK SCHOLES MODEL**

* **LOCAL VOLATILITY MODEL**





* **STOCHASTIC VOLATILITY INSPIRED MODEL**



* **SURFACE STOCHASTIC VOLATILITY INSPIRED MODEL**

* **RANDOM VARIABLE SIMULATOR**

* **MONTE CARLO COMPUTER**

* **CURVE INTERPOLATION** 

* **SURFACE INTERPOLATION**



* **FAST INTEGRAL COMPUTATION**



* **FAST RANDOM INTEGRAL COMPUTATION**

* **ROOTFINDER**

* **TIMER**

## Contributing

Any contributions are **greatly appreciated**

1. Fork the Project
2. Create your Feature Branch (`git checkout -b myBranch`)
3. Commit your Changes (`git commit -m '* Add a feature.'`)
4. Push to the Branch (`git push origin myBranch`)
5. Open a Pull Request

## License

See `LICENSE` for more information.

## Contact

Matthieu Charrier - [@mattcharr](https://www.linkedin.com/in/matthieu-charrier-080820134/) - matthieu.charrier.pro@gmail.com

Project Link: [https://github.com/matt-charr/QA](https://github.com/matt-charr/QA)

[contributors-shield]: https://img.shields.io/github/contributors/matt-charr/QA.svg?style=for-the-badge
[contributors-url]: https://github.com/matt-charr/QA/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/matt-charr/QA.svg?style=for-the-badge
[forks-url]: https://github.com/matt-charr/QA/network/members
[stars-shield]: https://img.shields.io/github/stars/matt-charr/QA.svg?style=for-the-badge
[stars-url]: https://github.com/matt-charr/QA/stargazers
[issues-shield]: https://img.shields.io/github/issues/matt-charr/QA.svg?style=for-the-badge
[issues-url]: https://github.com/matt-charr/QA/issues
[license-shield]: https://img.shields.io/github/license/matt-charr/QA.svg?style=for-the-badge
[license-url]: https://github.com/matt-charr/QA/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/matthieu-charrier-080820134/