# 031 Api Versioning

## Lecture

[![# Api Versioning](https://img.youtube.com/vi/wYPpizfjVX8/0.jpg)](https://www.youtube.com/watch?v=wYPpizfjVX8)

## Instructions

At the beginning of this lesson, the existing `AuthenticationController.cs` and `UserDto.cs` have been versioned to `V1`. To complete this lesson you will need to implement `V2`. To do this, you will need to make use of `FullAddress.cs` and `FullAddressDto.cs` which have also been pre-defined for you. Do NOT change any of these files, doing so will cause autograding for the lesson to fail.

In `HomeEnergyApi/Program.cs`
- To the builder's services add the following Api Versioning options / values
    - `AssumeDefaultVersionWhenUnspecified` / `true`
    - `DefaultApiVersion` / `new ApiVersion(1, 0)`
    - `ReportApiVersions` / `true`

In `HomeEnergyApi/Dtos/UserDtoV2.cs`
- Create a new public class `UserDtoV2` with the following public property names / types
    - Username / string
    - Password / string
    - Role / string
    - Address / FullAddress (from `HomeEnergyApi/Models/FullAddress.cs)

In `HomeEnergyApi/Controllers/AuthenticationV2Controller.cs`
- Start by copying and pasting all code from `HomeEnergyApi/Controllers/AuthenticationV1Controller.cs`
- Replace any instance of `AuthenticationV1Controller` in this file, with `AuthenticationV2Controller`
    - Ensure you are ONLY changing the file `AuthenticationV2Controller.cs`
- Replace any instance of `UserDtoV1` in this file with `UserDtoV2`
- Modify the `ApiVersion` attribute on `AuthenticationV2Controller` to set the Api Version to `2.0`
- Add a new private method `BuildFullAddress()` to `AuthenticationV2Controller`, with a return type of `string`
    - `BuildFullAddress()` should take one argument of type `UserDtoV2`
    - `BuildFullAddress()` should read the `StreetAddress`, `City` and `ZipCode` property on the `Address` property of the passed `UserDtoV2` and arrange them like so `"{userDto.Address.StreetAddress} {userDto.Address.City}, {userDto.Address.ZipCode}"`
        - `StreetAddress` and `City` are seperated by " "(one space), `City` and `ZipCode` are seperated by ", "(one comma followed by one space) with no leading or trailing characters
        - So if `StreetAddress` was "678 Maple Ave.", `City` was "Springfield", and `Zipcode` was "85926", `BuildFullAddress()` would return `678 Maple Ave. Springfield, 85926`
- Modify the `Register()` method so that...
    - The value being passed to `ValueEncryptor.Encrypt()` is changed to the result of calling `BuildFullAddress()`, passing the `UserDtoV2` retreived from the body of the HTTP request

In `HomeEnergyApi/Models/User.cs`
- Add a property `EncryptedAddress` of type `string` to `User`

In `HomeEnergyApi/Dtos/HomeProfile.cs`
- Add a map from `UserDtoV2` to `User`, by adding a new `CreateMap()` call

## Additional Information
- Do not remove or modify anything in `HomeEnergyApi.Tests`
- Some Models may have changed for this lesson from the last, as always all code in the lesson repository is available to view
- Along with `using` statements being added, any packages needed for the assignment have been pre-installed for you, however in the future you may need to add these yourself

## Building toward CSTA Standards:
- Design and iteratively develop computational artifacts for practical intent, personal expression, or to address a societal issue by using events to initiate instructions (3A-AP-16) https://www.csteachers.org/page/standards
- Demonstrate code reuse by creating programming solutions using libraries and APIs (3B-AP-16) https://www.csteachers.org/page/standards
- Plan and develop programs for broad audiences using a software life cycle process (3B-AP-17) https://www.csteachers.org/page/standards
- Use version control systems, integrated development environments (IDEs), and collaborative tools and practices (code documentation) in a group software project (3B-AP-20) https://www.csteachers.org/page/standards
- Modify an existing program to add additional functionality and discuss intended and unintended implications (e.g., breaking other functionality) (3B-AP-22) https://www.csteachers.org/page/standards

## Resources
- https://github.com/dotnet/aspnet-api-versioning

Copyright &copy; 2025 Knight Moves. All Rights Reserved.
