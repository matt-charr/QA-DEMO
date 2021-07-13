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
    <li><a href="#features">Features</a></li>
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

The core of the technology is located on GitHub with a restricted access.

In case you wish to contribute and share interesting addons of functionality, please kindly contact the owner to explain your addins. Subject to approval, a fixed time limited access will be granted.

If you wish more information about this project, go to the paragraph "features".

### Installation

Once you received your access, you simply need to clone this repository to your machine:

```sh
mkdir my_QA
cd my_QA
git clone https://github.com/matt-charr/QA.git
```

### Compilation

To compile the project, it is necessary to have CMake installed on your machine.
It is recommended to make a *bin* directory to store the executables and a *build* directory to store the makefiles.

```sh
cd my_QA
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

## Features

The project contains several functionnalities. Please find below a non exhaustive list:

### MARKET DATA IMPORTER

You can import market data from a market data file you can create and drop in *data/internal/*. This file must contains lines of observables such as:

SPOT;*fixing_date*;*underlying*;*quote* \
RISK_FREE_RATE;*fixing_date*;*quote* \
REPO;*fixing_date*;*underlying*;*quote* \
VOLATILITY;*fixing_date*;*underlying*;*quote* \
CORRELATION;*fixing_date*;*underlying1*;*underlying2*;*quote* \
iVOLATILITY;*fixing_date*;*underlying*;*maturity*;*moneyness*;*bid*;*ask* \
iREPO;*fixing_date*;*underlying*;*maturity*;*bid*;*ask* \
FORWARD;*fixing_date*;*underlying*;*maturity*;*quote* \
OPTION;*fixing_date*;*underlying*;*maturity*;*strike*;*call_bid*;*call_ask*;*put_bid*; *put_ask*

All dates must respect the format *%Y-%m-%d*.

Once you have your market data file well located, you can download it into your code using:

```cpp
market_data<object::Data> src;
downloader ("../data/internal/filename.csv", src);
```

* Extract implied volatility data of the ticker ^AAPL at 2021-05-25 with maturity 2022-07-15:

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

* Extract data from CBOE.

You can download the market data file of your favorite ticker at your birthday in [CBOE](https://www.cboe.com/), rename by *CBOE_MyTicker_%Y-%m-%d.csv*  and drop it to *data/external/*. The following functions will extract all the information of te file, drag options data to *option* and spot data to *spot*

```cpp
extract_information_from_cboe (Date ("1994-05-23"), Underlying ("^AAPL"), option, spot);   
```

 Convert option data to implied volatility.

Suppose you have spot and option data and you wish to extract implied volatilities and drop it into *src*.

```cpp
convert_option_to_implied_volatility (option, spot, src);
```

 Plot implied volatility slice and surface.

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

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image1.PNG" alt="Logo" width="600" height="450">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image2.png" alt="Logo" width="600" height="450">    

</p>

### CONTRACT ALGEBRA

You can write any financial contract (except choosing style product) by:

**Contract (*trading_date*, *cashflow*)** 

and using the following combinator:

**Amount combinator**

**CASH** (cash) \
**SPOT** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**AVERAGE** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**BEST** (*underlyings*, *fixing_date*) \
**INDEX** (*underlyings*, *fixing_date*, *weights*) \
**MAXIMUM** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**MINIMUM** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**VARIANCE** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**RANGE** (*underlying*, *fixing_date*, *start_date*, *end_date*, *frequency*) \
**PERFORMANCE** (*underlying*, *fixing_date*, *start_date*, *end_date*) \
**COVARIANCE** (*underlying1*, *underlying2*, *fixing_date*, *start_date*, *end_date*, *frequency*) 

**CashFlow combinator**

**PAY** (*amount*, *payment_date*) \
**END** (*maturity_date*) 

**Event combinator**

**KNOWN** (*binary*) \
**IF** (*event*) (*cashflow_then*, *cashflow_else*) 

**Arithmetic combinator**

**POW** (*amount*, *integer*) \
**MAX** (*amount*, *amount*) \
**MIN** (*amount*, *amount*) \
**ABS** (*amount*) \
**COS** (*amount*) \
**SIN** (*amount*) \
**TAN** (*amount*) \
**EXP** (*amount*) \
**LOG** (*amount*) 

Additionnaly you can add/sub cashflow/contract with same or different payment_date/schedule, multiply them by a constant or take the opposite to create more complex contract.

For example, a call on *my_underlying* beginning at *%Y-%m-%d*, with maturity *%Y'-%m'-%d'* and strike *my_strike* is:

```cpp
auto my_contract = Contract (
  Date ("%Y-%m-%d"),
  PAY (
    MAX (
      SPOT (Underlying (my_underlying), Date ("%Y'-%m'-%d'")) - my_strike,
      CASH (0.0)
    ),
    Date ("%Y'-%m'-%d'")
  )
);
```

* Print a contract.

```cpp
printf (my_contract);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image3.PNG" alt="Logo" width="600" height="450">

</p>

* Extract payment dates.

```cpp
std::vector<Date*> dates;
contract.payment_dates(dates);
for (auto date : dates) printf (*date);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image4.PNG" alt="Logo" width="600" height="450">

</p>

* Extract fixing dates.

```cpp
std::vector<Date*> dates;
contract.fixing_dates(dates);
for (auto date : dates) printf (*date);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image5.PNG" alt="Logo" width="600" height="450">

</p>

* Extract underlyings.

```cpp
std::vector<Underlying*> underlyings;
contract.underlyings(underlyings);
for (auto underlying : underlyings) printf (*underlying);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image6.PNG" alt="Logo" width="600" height="450">

</p>

* Extract relevent observables.

```cpp
std::vector<Component*> observables;
contract.observables(observables);
for (auto observable : observables) printf (*observable);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image7.PNG" alt="Logo" width="600" height="450">

</p>

* Time travelling.

After pushing back a quote for *my_underlying* on *%Y-%m-%d* to the market data file. 
*my_contract* integrates it in its description and *move* method return the same contract at the desired date:

```cpp
auto my_future_contract = my_contract.move (Date ("%Y-%m-%d"), my_market_data);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image8.PNG" alt="Logo" width="600" height="450">

</p>

* Try to find a closed form price.

```cpp
contract.closed_form_pricer(&my_model);
```

* Delete.

```cpp
my_contract.erase ();
```

### MONTE CARLO INSPECTOR

You can create a monte carlo inspector with:

```cpp
auto basis = BASIS365;
auto my_step = new NumberOfDays (10);
auto my_monte_carlo_inspector = MonteCarloInspector (
    new DefaultAssetSampler (
        &my_contract,
        &my_model,
        &my_discount_curve,
        my_step,
        my_basis
    )
);
```

*my_basis* can be either *BASIS360* or *BASIS365* and *my_step* is a *unsigned* * element, if the last one is set to *NULL*, fixing dates will be used as path dates and no discretization will be handled.

* Refiner.

```cpp
auto size = 100000;
auto verbose = true;
my_monte_carlo_inspector.refine (size, verbose);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image9.PNG" alt="Logo" width="600" height="450">

</p>

* Ultimate size refiner.

```cpp
auto size = 100000;
auto batch_size = 1000;
auto verbose = true;
my_monte_carlo_inspector.refine_until_size (size, batch_size, verbose);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image10.PNG" alt="Logo" width="600" height="450">

</p>

* Ultimate precision refiner.

```cpp
auto precision = 1e-5;
auto batch_size = 1000;
auto verbose = true;
my_monte_carlo_inspector.refine_until_precision (precision, batch_size, verbose);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image11.PNG" alt="Logo" width="600" height="450">

</p>

* Convergence viewer.

```cpp
my_monte_carlo_inspector.plot_convergence ();
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image12.PNG" alt="Logo" width="600" height="450">

</p>

* Price distribution viewer.

```cpp
my_monte_carlo_inspector.plot_price_distribution ();
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image13.PNG" alt="Logo" width="600" height="450">

</p>

* MonteCarlo historical result printer.

```cpp
my_monte_carlo_inspector.show ();
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image14.PNG" alt="Logo" width="600" height="450">

</p>

* Density of relevent observables viewer.

```cpp
my_monte_carlo_inspector.plot_observable_distribution ();
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image15.PNG" alt="Logo" width="600" height="450">

</p>

* Maturity distribution printer.

```cpp
my_monte_carlo_inspector.print_maturity_distribution ();
```

### PARTIAL DIFFERENTIAL EQUATION INSPECTOR

Up to now, this framework is available only for vanilla products.
To create a partial differential equation pricer, you simply need to delcare:

```cpp
auto my_xmin = log (0.5);
auto my_xmax = log (1.5);
auto my_nx = 25;
auto my_nt = 10;
auto my_left_bound = [] (double time) { return 0.0; };
auto my_right_bound = [] (double time) { return 0.0; };
auto my_basis = BASIS365;
auto my_boundary_type = "Neumann";
auto my_scheme = 1.;
my_partial_differential_equation_inspector.solve (
    my_xmin, 
    my_xmax,
    my_nx,
    my_nt,
    my_left_bound,
    my_right_bound,
    my_basis,
    my_boundary_type,
    my_scheme
);
```

*my_xmin* and *my_xmax* corresponds to the bounds of the space grid and *my_nx* is the number of points contained in the space grid.
*my_scheme* corresponds to the *theta* parameter in theta schemes and *my_boundary_type* is the boundary style (Neumann or Dirichlet).
If *my_boundary_type* is "Dirichlet", *my_left_bound* (resp. *my_right_bound*) are deterministic functions of time and corresponds to the value function on the left (resp. right) hand side of the grid.
Else *my_boundary_type* is "Neumann", *my_left_bound* (resp. *my_right_bound*) are deterministic functions of time and corresponds to the derivative function on the left (resp. right) hand side of the grid.

* Price/Delta/Dollargamma/Theta function slice viewer

```cpp
auto my_style = "price"; // {price,delta, dollar_gamma, theta} 
auto my_fixing_date = Date ("%Y-%m-%d");
partial_differential_equation_inspector.plot_slice (my_style, my_fixing_date);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image16.PNG" alt="Logo" width="600" height="450">

</p>

* Price/Delta/Dollargamma/Theta function surface viewer

```cpp
auto my_style = "price"; // {price,delta, dollar_gamma, theta} 
auto my_start_date = Date ("%Y-%m-%d");
partial_differential_equation_inspector.plot_slice (my_style, my_start_date);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image17.PNG" alt="Logo" width="600" height="450">

</p>

### EQUITY MODEL

To declare a model *Model* written on names *my_underlying_1*, *my_underlying_2*, ...,
*my_underlying_n*.

```cpp
auto model = Model(
  {
    my_underlying_1,
    my_underlying_2,
    ...,
    my_underlying_n
  }
);
```

* Calibration.

To calibrate the model on a date *%Y-%m-%d* using market data *my_data*, you can run:

```cpp
model.calibration(Date("%Y-%m-%d"), my_data);
```

* Paths drawer.

Eventually, you can show *my_number_of_paths* scenarii between two dates *%Y-%m-%d* and *%Y'-%m'-%d'* with a frequency of *my_number_of_days* for the asset under this model:

```cpp
auto my_number_of_paths = 10;
auto my_number_of_days = 1;
model.draw_path(Date("%Y-%m-%d"), Date("%Y'-%m'-%d'"), my_number_of_paths, my_number_of_days);
```

**Equity model available**

```cpp
BlackScholesModel
MultiBlackScholesModel
LocalVolatilityModel
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image18.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image19.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image20.PNG" alt="Logo" width="600" height="450">

</p>

### VOLATILITY MODEL

To declare a model *Model*, you need one underlying *my_underlying* and run:

```cpp
auto model = Model(my_underlying);
```

* Calibration.

To calibrate the model on a date *%Y-%m-%d* using market data *my_data*, you can run:

```cpp
model.calibration(Date("%Y-%m-%d"), my_data);
```

* Slice and surface viewer.

```cpp
model.plot_slice (Date("%Y-%m-%d"));
model.plot_surface (Date("%Y-%m-%d"), Date("%Y'-%m'-%d'"));
```

**Volatility model available**

```cpp
SurfaceStochasticVolatilityInspiredModel
RawStochasticVolatilityInspiredModel
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image21.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image22.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image23.PNG" alt="Logo" width="600" height="450">

</p>

### CURVE INTERPOLATION 

To interpolate a curve, you first need to declare the serie of two dimensionnal points *my_points* yo want to connect (any order):

```cpp
Point2D my_points[] = {
  Point2D (1.0, 3.0),
  Point2D (2.5, 10.0),
  Point2D (0.0, 1.0)
};
```

Choose an interpolation style *MyInterpolationStyle*:

```cpp
auto number_of_points_to_interpolate = 3;
auto my_interpolation = MyInterpolationStyle (points, number_of_points_to_interpolate);
```

You can eventually assess the accuracy of interpolation:

```cpp
auto mumber_of_points_betwwen_two_consecutive_points = 100;
my_interpolation.plot (mumber_of_points_betwwen_two_consecutive_points);
```

The interpolation style available are:

```cpp
FlatInterpolation
LinearInterpolation
CubicSplinesInterpolation
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image24.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image25.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image26.PNG" alt="Logo" width="600" height="450">

</p>

### SURFACE INTERPOLATION

To interpolate a surface, you first need to declare the serie of three dimensionnal points *my_points* yo want to connect (any order):

```cpp
auto points = new Point3D [15];
for (unsigned i (0), n (0); i < 5; ++i)
{
    for (unsigned j (0); j < 3; ++j, ++n)
    {
        points [n] = Point3D (i, j, sin (i*j));
    }
}
```

Choose an interpolation style *MyInterpolationStyle*:

```cpp
auto number_of_points_to_interpolate = 15;
auto my_interpolation = MyInterpolationStyle (points, number_of_points_to_interpolate);
```

You can eventually assess the accuracy of interpolation:

```cpp
auto mumber_of_points_betwwen_two_consecutive_x = 10;
auto mumber_of_points_betwwen_two_consecutive_y = 10;
my_interpolation.plot (
  mumber_of_points_betwwen_two_consecutive_x,
  mumber_of_points_betwwen_two_consecutive_y
);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image27.PNG" alt="Logo" width="600" height="450">

</p>

### FAST (STOCHASTIC) INTEGRAL COMPUTATION

Integrate a real function on an interval [*my_left*, *my_right*] first consists in vectorizing the function:

```cpp
auto my_function = [](arma::dvec const& x) -> arma::dvec { 
    return 0.3989 * arma::exp (-0.5 * x % x); 
};
```

or in case of a stochastic integral:

```cpp
auto function = [](arma::dvec const& t, arma::dvec const& w) -> arma::dvec { 
    return 100.0 * arma::exp (0.2 * w - 0.04 * t); 
};
```

Then:

```cpp
auto my_integral = Integral (my_function, my_left, my_right);
```

* Ultimate size refiner.

```cpp
auto size = 10;
auto verbose = true;
my_integral.run_until_size (size, verbose);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image28.PNG" alt="Logo" width="600" height="450">

</p>

* Ultimate precision refiner.

```cpp
auto precision = 1e-5;
auto verbose = true;
my_integral.run_until_precision (precision, verbose);
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image29.PNG" alt="Logo" width="600" height="450">

</p>

* Convergence viewer.

```cpp
my_integral.plot ();
```

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image30.PNG" alt="Logo" width="600" height="450">

</p>

<p align="center">

  <img src="https://github.com/matt-charr/QA-DEMO/blob/main/image31.PNG" alt="Logo" width="600" height="450">

</p>

## Contributing

Any contributions are greatly appreciated

1. Fork the Project
2. Create your Feature Branch (`git checkout -b myBranch`)
3. Commit your Changes (`git commit -m '* Add a feature.'`)
4. Push to the Branch (`git push origin myBranch`)
5. Open a Pull Request

## License

See `LICENSE` for more information.

## Contact

Matthieu Charrier - [@mattcharr](https://www.linkedin.com/in/matthieu-charrier-080820134/) - matthieu.charrier.pro@gmail.com

Project Link (make sure your access rights before browsing): [https://github.com/matt-charr/QA](https://github.com/matt-charr/QA)

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