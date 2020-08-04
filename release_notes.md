# Release Notes

--------------------------------------------------------------------------------
# Release v1.2.0
- component refresh removed as it is now automatic in variable change
- functions return values corrected

# Release v1.1.0
-NexText::appendText function added

# Release v1.0.0

- Added support for multiple nextion displays
  - Recommendation initialize nextion instance using Nextion::GetInstance command Harware and Software interfaces supported
  - Nextion objects requires pointer to intance.
  - Instance callback functiona must be initialized to instance object.
- implementation divided to ./src ans ./include folders
- STD_SUPPORT define replased with platform ESP8266 define if other platforms suppors needed std functionality add platform define with or (||)
- TFT file upload added to behing of NEX_ENABLE_TFT_UPLOAD define
- Documentation updated.
- Examples updated.
- platformIO development platformio.ini and .library.json added
- Version numbering uses now Semantic Versioning 1.0.0 (https://semver.org/)
  -Given a version number MAJOR.MINOR.PATCH, increment the:
    MAJOR version when you make incompatible API changes,
    MINOR version when you add functionality in a backwards compatible manner, and
    PATCH version when you make backwards compatible bug fixes.
