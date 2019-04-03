<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/stevenwhitespacesystems/fm-mime-types">
    <img src="logo-alt.png" alt="Logo" width="140" height="104">
  </a>

  <h3 align="center">fm-mime-types</h3>

  <p align="center">
    Returns a MIME-type string from a filename on the FileMaker Pro Platform.
    <br />
    <a href="https://github.com/stevenwhitespacesystems/fm-mime-types"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/stevenwhitespacesystems/fm-mime-types/issues">Report Bug</a>
    ·
    <a href="https://github.com/stevenwhitespacesystems/fm-mime-types/issues">Request Feature</a>
  </p>
</p>

<!-- PROJECT SHIELDS -->
[![FileMaker Version][filemaker-shield]]()
[![FileMaker Platform][platform-shield]]()
[![Commit Shield][commit-shield]]()
[![Contributors][contributors-shield]]()
[![MIT License][license-shield]][license-url]
[![Facebook][facebook-shield]][facebook-url]
[![LinkedId][linkedin-shield]][linkedin-url]

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Built With](#built-with)
* [Features](#features)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
    * [Version](#version)
    * [Limitations](#limitations)
* [Usage](#usage)
  * [Installation](#installation)
  * [Quick Start](#quick-start)
  * [Sample Conversions](#sample-conversions)
  * [Parameters](#parameters)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)
* [fmapi Product Suite](#fmapi-product-suite)
  * [fmapi Apps](#fmapi-apps)

<!-- ABOUT THE PROJECT -->
## About The Project

<p align="center">
  <a href="https://github.com/stevenwhitespacesystems/fm-xml2json">
    <img src="logo.png" alt="Logo" width="580" height="208">
  </a>
</p>

As we delved into the world of REST APIs using FileMaker, we stumbled across an issue.

> *How do we get a file's MIME-type in FileMaker Pro?*

When you are dealing with binary data and having to send HTTP Headers in relation to this data, you will most certainly have to provide a `Content-Type` header at some point.

This header tells the recipient the type of information that is being passed over the network.

e.g. A pdf file will have the Content-Type of `application/pdf`.

We found out during our development of [fmapi-aws-s3](https://whitespacesystems.co.uk/portfolio-item/filemaker-aws-s3-integration/) that to put data onto an S3 bucket, we would have to pass in the MIME-type of the file we send.

This was an issue and with any issue, solutions are born.

We present `fm-mime-types`.

A FileMaker script which when passed a **valid** filename, will return the correct MIME-type for that file format.

### Built With
* [FileMaker Pro](https://www.filemaker.com/)
* No 3rd party plugins.

<!-- FEATURES -->
## Features

* **Backwards Compatible**:
This script has been designed to be backwards compatibile to FileMaker Pro 12!

* **Small Code Base**:
We've optimised our code as much as possible which has resulted in the script being less than 50 script lines.

* **Extremely Fast**:
With optimisation comes efficiency. Our testings show that the script runs at less than **500ms** on the first run. Subsequent runs after it's cached the mime-db.json run, consistently, at **~50ms**. *These tests where run on the script locally. Networked usage may differ.*

* **No Dependencies**:
This script is fully dependent and requires no plugins.

<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

#### Version

The FileMaker script makes use of the [Insert from URL](https://fmhelp.filemaker.com/help/17/fmp/en/index.html#page/FMP_Help/insert-from-url.html) script step introduced in FileMaker 12.

This means that this script will only work with **FileMaker 12+** products.

Using the script with anything less than 12 will have unexpected behaviour.

#### Limitations

##### FileMaker Text Parsing Functions

We have built the rules for identifying MIME-types in FileMaker using all the Text Functions available to us and from our testing it has handled all the filenames thrown at it.

However, there may be some fringe cases where this breaks down. If you discover such a case, please create a [Bug Report](https://github.com/stevenwhitespacesystems/fm-xml2json/issues) and we'll see if we can correct it. Unfortunately, there may be cases that can't be solved.

<!-- USAGE EXAMPLES -->
## Usage

### Installation

1. Copy the `fm-mime-types` script to your solution.

It's that simple.

### Quick Start

There are 2 fmp12 files provided here

1. fm-mime-types.fmp12
2. fm-mime-types-tests.fmp12

`fm-mime-types.fmp12` file contains the script that you need to copy over.
  
`fm-mime-types-tests.fmp12` file contains our test suite to confirm that the script behaves as intended.

If you open the `fm-mime-types` file, you can drag a file onto a container field or enter a filename manually and get the MIME-type by pressing the `Get MIME-type` button.

### Sample Conversions

| filename | MIME-type 
|:----|:----------------|
| `test.pdf` | `application/pdf`
| `test.pdf.zip` | `application/zip`
| `test.js` | `application/javascript`
| `image.png` | `image/png`

### Parameters

The parameters below can be used as for the script. Each parameter has to be followed by a carriage return (¶). The table below will state it's position in the parameters list.

| Position | `name` | Description |
|:---------|:-------|:------------|
| 1 | `Filename` | This is a full filename of file you are trying to get a MIME-type of e.g. `image.png`
| 2 | `Object Name` | **FileMaker 15 or less ONLY** Insert From URL requires a field in FM < 16. Give a field on the current context an object name. This script is smart enough to set the field and then clear it out once it's done with it. *Tip: Use a global field*
| 3 | `Object Repetition` | **FileMaker 15 or less ONLY** Repitition number of Object Name value above. This parameter defaults to 1 so can be ignored if not required.

Here are 2 examples of what you'd pass the `fm-mime-types` script.

#### FileMaker <= 15

```javascript
List (
  "image.png" ;
  "fm-mime-type-object" ;
  1
)
```
*Where `fm-mime-type-object` is the object name of a field on the current layout.*

#### FileMaker >= 16
```javascript
"image.png"
```

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.

<!-- CONTACT -->
## Contact

Steven McGill - [WhiteSpace Systems Ltd](https://whitespacesystems.co.uk) - [steven@whitespacesystems.co.uk](mailto:steven@whitespacesystems.co.uk)

Project Link: [fm-mime-types](https://github.com/stevenwhitespacesystems/fm-mime-types)

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [MIME-db](https://github.com/jshttp/mime-db)
* [Computech IT Services](https://www.computech-it.co.uk)
* [Best-README-Template](https://github.com/othneildrew/Best-README-Template)

<!-- FMAPI SUITE -->
## fmapi Product Suite

When FileMaker 16 introduced cURL with the Insert from URL script step. Use cases for FileMaker Pro increased dramatically in relation to REST APIs.

It allowed developers to finally communicate with other web services and APIs without the need for 3rd party plugins. Integration with Couriers, Payment Gateways & Social Media Sites all became within touching distance.

However, without prior knowledge of cURL, HTTP Request Methods, HTTP Headers, JSON, OAuth Authentication, API Keys, API documentation etc, it can be extremely difficult to get started for the novice user or even the most proficient FileMaker developer.

And with that comes our goal, to simplify communications between your FileMaker App and the vast amount of Web Services available, no matter your ability level.

Read more over at [What is fmapi?](https://whitespacesystems.co.uk/filemaker-3rd-party-api-integration/)

### fmapi Apps

A collection of FileMaker apps that communicate directly with popular 3rd party REST APIs.

* [fmapi-vies-vat](https://whitespacesystems.co.uk/portfolio-item/filemaker-vies-vat-integration/) - Integrate the EU Commissions Vies VAT API directly into you FileMaker App allowing you to validate EU VAT Numbers.

<!-- MARKDOWN LINKS & IMAGES -->
[filemaker-shield]: https://img.shields.io/badge/filemaker-%3E%3D%2012.0.0-009edb.svg
[platform-shield]: https://img.shields.io/badge/platform-Pro%20%7C%20Go%20%7C%20Server%20%7C%20Webdirect%20%7C%20Cloud-purple.svg
[contributors-shield]: https://img.shields.io/github/contributors/stevenwhitespacesystems/fm-mime-types.svg
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg
[commit-shield]: https://img.shields.io/github/last-commit/stevenwhitespacesystems/fm-mime-types.svg
[license-url]: https://choosealicense.com/licenses/mit
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?logo=linkedin&colorB=0077B5
[linkedin-url]: https://www.linkedin.com/company/whitespace-systems-ltd/
[facebook-shield]: https://img.shields.io/badge/-facebook-white.svg?logo=facebook&colorB=3578E5
[facebook-url]: https://www.facebook.com/WhitespaceSystemsLtd/