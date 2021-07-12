[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

<br />
<p align="center">
  <a href="https://github.com/matt-charr/QA-DEMO">
    <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image.jpg" alt="Logo" width="400" height="300">
  </a>

  <h3 align="center"><strong>QA</strong></h3>

  <p align="center">
    <em>Quantitative Analytics</em>
    <br />
    <a href="https://github.com/matt-charr/QA"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/matt-charr/QA/tree/master/test">View Demo</a>
    ·
    <a href="https://github.com/matt-charr/QA/issues">Report Bug</a>
    ·
    <a href="https://github.com/matt-charr/QA/pulls">Request Feature</a>
  </p>
</p>


<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-project">Genesis</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

## Genesis

As all <a href="https://www.merriam-webster.com/words-at-play/padawan-the-new-intern"><em>Padawan</em></a> has the responsability to improve his  understanding of <a href="https://fr.wikipedia.org/wiki/Force_(Star_Wars)"><em>The Force</em></a>, it is the duty of all quants, from junior to senior, to constantly deepen his understanding of quantitative finance. 

The aim of this repository is to efficiently design a cutting-edge technology for market finance which, as discovering interesting theoretical concepts closely studied from masterbooks, will be fortified.

I began this project while I was receiving the wonderful teaching from <a href="https://business-cool.com/decryptage/analyse/master-el-karoui-le-master-phare-pour-integrer-le-monde-de-la-finance-analytique/"><em>The Temple</em></a>.

Feel free to contribute and/or share interesting addons of functionality.

## Getting Started

### Market Data

This project uses market data provided by the below websites

* [CBOE](https://www.cboe.com/) - spot and option data 
* [EUREX](https://www.eurex.com/) - spot and option data
* [IBORATE](http://iborate.com/eur-libor/) - LIBOR data
* [SEBGROUP](https://sebgroup.com/) - SWAP data

In particuler, the user can download spot and options data of his favorite ticker from the below sources, drop the excel file in the directory and rename it following closely the name convention.  <a href="https://github.com/matt-charr/QA/tree/master/data"><em>data/</em></a> 

### Installation

In order to install the package, you simply need to clone this repository to your machine

  ```sh
  mkdir Ho-Oh
  cd Ho-Oh
  git clone https://github.com/matt-charr/QA.git
  ```

To compile the project, it is necessary to have CMake installed within your machine.

  ```sh
  cd Ho-Oh
  mkdir build bin
  cd build/
  cmake -G "MinGW Makefiles" ..
  make .
  ```

## Tools

Go to the folder <a href="https://github.com/matt-charr/QA/tree/master/test"><em>test/</em></a> to test all the functionnalities provided by the project

* **BLACK SCHOLES MODEL AND ITS TRICKS**
* **CONTRACT ALGEBRA**
* **FLAT, LINEAR AND CUBIC SPLINE INTERPOLATION** 
* **GREEKS DISCOVERER**
* **FAST INTEGRAL COMPUTATION**
* **FAST RANDOM INTEGRAL COMPUTATION**
* **LINEAR PARTIAL DIFFERENTIAL EQUATION SOLVER**
* **MULTI BLACK SCHOLES MODEL AND ITS TRICKS**
* **LOCAL VOLATILITY MODEL AND ITS TRICKS**
* **MARKET DATA FINDER**
* **RANDOM VARIABLE SIMULATOR**
* **MONTE CARLO COMPUTER**
* **MONTE CARLO EXPLORER**
* **PARTIAL DIFFERENTIAL EQUATION PRICER (1D)**
* **STATIC REPLICATION PRICER (1D)**
* **ROOTFINDER**
* **STOCHASTIC VOLATILITY INSPIRED MODEL**
* **SURFACE STOCHASTIC VOLATILITY INSPIRED MODEL**
* **GENERAL SURFACE INTERPOLATION**
* **TIMER**

## Roadmap

See the [open issues](https://github.com/matt-charr/QA/issues) for a list of proposed features (and known issues).

## Contributing

Any contributions are **greatly appreciated**

1. Fork the Project
2. Create your Feature Branch (`git checkout -b myBranch`)
3. Commit your Changes (`git commit -m 'add a feature'`)
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