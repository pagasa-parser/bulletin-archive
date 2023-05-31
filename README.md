# PAGASA Bulletin Archive
This repository contains a near-complete collection of Severe Weather Bulletins (SWBs), Tropical Cyclone Bulletins (TCBs), and Tropical Cyclone Advisories (TCAs) issued by PAGASA from late 2020 to the present. These archives are mirrored from the Internet Archive which are, in turn, collected from PAGASA. See [Infrastructure](#infrastructure) for more information.

This repository exists for the purpose of mass-testing PAGASA Parser tools with every single SWB and TCB, ensuring that a wide range of cases are accomodated. This helps future-proof these tools, and ensures proper delivery of data.

This is a Git mirror of the archives [hosted on the Internet Archive](https://archive.org/details/@chlodalejandro?tab=uploads&and%5B%5D=subject%3A%22severe+weather+bulletin%22&and%5B%5D=subject%3A%22tropical+cyclone+advisory%22&and%5B%5D=subject%3A%22tropical+cyclone+bulletin%22&sort=-publicdate). The Internet Archive contains derived versions, including image renders. This repository only contains the original bulletin PDF files from the archive.

## Structure
Every bulletin is organized by storm in the `archive/` folder. The folder names mirror their Internet Archive identifiers (explained in [Infratstructure](#infrastructure)) and only contain PDF versions of the data.

Filenames follow the format `PAGASA_YY_TCXX_StormName_TCB#NN.pdf`:
* `YY` is the last two digits of the year (`23` for 2023, etc.).
* `XX` is the ordinal number of the storm in the Philippines' storm naming list.
 * Since the list is alphabetical, this means `TC01` is the first storm of the year with a name starting in "A", `TC02` is the second storm of the year with a name starting in "B", and so on.
* `StormName` is the local (Philippine; PAGASA-designated) name of the storm. This is also the case for Tropical Cyclone Advisories which eventually formed as storms in or entered the Philippine Area of Responsibility.
* `TCB` determines the bulletin type. `SWB` refers to a Severe Weather Bulletin, `TCB` refers to a Tropical Cyclone Bulletin, and `TCA` refers to a Tropical Cyclone Advisory (only supplied if the storm was previously tracked as a tropical cyclone within the [Tropical Cyclone Advisory Domain](https://en.wikipedia.org/wiki/Philippine_Area_of_Responsibility#Other_areas_forecasting_domains), or TCAD).
* `NN` is the bulletin number, zero-padded.

The final bulletin is always prepended with `-FINAL` after the bulletin number. Special bulletins, numbered `2A` or similar, have the extra letters removed.

## Updating
This repository can be updated with one click using GitHub Actions. This is restricted only for repository members.

Should you wish to update manually, or if you want to update your local copy, ensure that you have Python, pip, and the `internetarchive` pip package installed. Afterwards, run the following command in the `archive/` folder.

```bash
ia download --search="uploader:chlodaidanalejandro@hotmail.com (subject:bulletin)" --glob="*.pdf"
```

## Infrastructure
These archives are the slowest-updating and come after the rest of the following chain:
* All bulletins originate from [PAGASA's File Repository](https://pubfiles.pagasa.dost.gov.ph/tamss/weather/bulletin/), usually updated first. In most cases, it is updated at the same time that the [bulletin webpage](https://bagong.pagasa.dost.gov.ph/tropical-cyclone/severe-weather-bulletin) is updated. This list of files is the same as the list found at the bottom of the bulletin webpage.
* Once bulletins are posted, [Zoomiebot](https://zoomiebot.toolforge.org/) checks the proper folder every 10 minutes for new updates. Since bulletins are almost never posted on the dot, this interval ensures that bulletins are collected at least 10 minutes after they've been posted.
 * For the first bulletin, a relevant item is made on the Internet Archive, under the identifier `pagasa-YY-TCXX`, where `YY` is the last two digits of the year (`23` for 2023, etc.) and `XX` is the ordinal number of the storm in the Philippines' storm naming list.
 * For subsequent bulletins, the relevant item is updated.
* Manual workflow dispatches on this repository update this repository on an as-needed basis. Should you wish to download bulletins through Git but also ensure that it is up-to-date, see the [Updating](#updating) section.

## Copyright
Official works created by an employee or by multiple employees of the Government of the Philippines are under Public Domain unless otherwise stated. These archives provided are subject to Part IV, Chapter I, Section 171.11 and Part IV, Chapter IV, Section 176 of Republic Act No. 8293 and Republic Act No. 10372, as amended.

Due to the humanitarian nature of these documents, the PAGASA Parser project aims to keep all related tools and infrastructure open source and free for any use. This README file is licensed under the [Creative Commons Attribution-ShareAlike 3.0 Unported License](https://creativecommons.org/licenses/by-sa/3.0/).