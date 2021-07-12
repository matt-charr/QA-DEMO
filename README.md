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

<br>SPOT;*fixing_date*;*underlying*;*quote*<br>
<br>RISK_FREE_RATE;*fixing_date*;*quote*<br>
<br>REPO;*fixing_date*;*underlying*;*quote*<br>
<br>VOLATILITY;*fixing_date*;*underlying*;*quote*<br>
<br>CORRELATION;*fixing_date*;*underlying1*;*underlying2*;*quote*<br>
<br>iVOLATILITY;*fixing_date*;*underlying*;*maturity*;*moneyness*;*bid*;*ask*<br>
<br>iREPO;*fixing_date*;*underlying*;*maturity*;*bid*;*ask*<br>
<br>FORWARD;*fixing_date*;*underlying*;*maturity*;*quote*<br>
<br>OPTION;*fixing_date*;*underlying*;*maturity*;*strike*;*call_bid*;*call_ask;*put_bid*; *put_ask*<br>

Once you have your market data file well located, you can download it into your code using:

```cpp
market_data<object::Data> src;
downloader ("../data/internal/filename.csv", src);
```

** Extract implied volatility data of the ticker ^AAPL at 2021-05-25 with maturity 2022-07-15:

```cpp
market_data<object::ImpliedVolatility> dst;
find<object::Data, object::ImpliedVolatility> (
    src,
    dst,
    [] (object::Data const& data) 
    {
        return (
            data.match_fixing_date (Date ("2021-05-25")) &&
            data.match_underlying (Underlying ("^AAPL")) &&
            data.match_maturity (Date ("2022-07-15"))
        );
    }
);    
```

*dst* will contain the data. 

** Extract data from CBOE.

You can download the market data file of your favorite ticker at your birthday in [CBOE](https://www.cboe.com/), rename by *CBOE_MyTicker_%Y-%m-%d.csv*  and drop it to *data/external/*. The following functions will extract all the information of te file, drag options data to *option* and spot data to *spot*

```cpp
extract_information_from_cboe (Date ("1994-05-23"), Underlying ("^AAPL"), option, spot);   
```

** Convert option data to implied volatility.

Suppose you have spot and option data and you wish to extract implied volatilities and drop it into *src*.

```cpp
convert_option_to_implied_volatility (option, spot, src);
```

** Plot implied volatility slice and surface.

You can plot implied volatility slice and surface.

```cpp
find<object::Data, object::ImpliedVolatility> (
    src,
    dst,
    [] (object::Data const& data) 
    {
        return (
            data.match_fixing_date (Date ("2021-05-25")) &&
            data.match_underlying (Underlying ("^AAPL"))
        );
    }
);
plot_implied_volatility_slice(dst, Date ("2023-05-25"));
plot_implied_volatility_surface(dst);
```

** Demo.




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