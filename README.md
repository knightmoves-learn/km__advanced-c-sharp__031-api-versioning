# 030 Api Key

## Lecture

NO VIDEO ON YOUTUBE YET
[![# Api Key](https://img.youtube.com/vi/RTUTtORZ8nM/0.jpg)](https://www.youtube.com/watch?v=RTUTtORZ8nM)

## Instructions

The file `HomeEnergyApi/secrets.json` has been pre-filled with an "ApiKey" property, do NOT change this file

In `HomeEnergyApi/Middleware/ApiKeyMiddleware.cs`
- Create a public class `ApiKeyMiddleware` with the following property modifiers / types / names
    - private const / `string` / APIKEYNAME
        - Set to value "X-Api-Key"
    - private readonly / `RequestDelegate` / _next
    - private / `string` / apiKey
- Create a constructor for `ApiKeyMiddleware` taking two arguments of types `RequestDelegate` and `IConfiguration`
    - Set the `RequestDelegate` property to the passed `RequestDelegate`
    - Set the `string` property to the result of getting the "ApiKey" property from the passed `IConfiguration`
- Create a method `InvokeAsync()` on `ApiKeyMiddleware` taking one argument of type `HttpContext`
    - `InvokeAsync()` should set the passed `HttpContext.Response.StatusCode` to "401" on the passed, and on it also call `Response.WriteAsync()` passing the value "Api Key was not provided." and return from the method if the following condition is met...
        -The result of calling `HttpContext.Request.Headers.TryGetValue()` passing the property "APIKEYNAME" is false, while ALSO creating a variable with the `out` value
    - `InvokeAsync()` should set the passed `HttpContext.Response.StatusCode` to "403" on the passed, and on it also call `Response.WriteAsync()` passing the value "Unauthorized client." and return from the method if the following condition is met...
        -The api key that was returned as the `out` value from `TryGetValue()` is not equal to the property "apiKey"
    - `InvokeAsync()` should await the result of passing the passed `HTTPContext` to the "_next" property

In `HomeEnergyApi/Program.cs`
- Have the `app` use middleware of type `ApiKeyMiddleware`

## Additional Information
- Do not remove or modify anything in `HomeEnergyApi.Tests`
- Some Models may have changed for this lesson from the last, as always all code in the lesson repository is available to view
- Along with `using` statements being added, any packages needed for the assignment have been pre-installed for you, however in the future you may need to add these yourself

## Building toward CSTA Standards:
- Give examples to illustrate how sensitive data can be affected by malware and other attacks (3A-NI-05) https://www.csteachers.org/page/standards
- Recommend security measures to address various scenarios based on factors such as efficiency, feasibility, and ethical impacts (3A-NI-06) https://www.csteachers.org/page/standards
- Compare various security measures, considering tradeoffs between the usability and security of a computing system (3A-NI-07) https://www.csteachers.org/page/standards
- Explain tradeoffs when selecting and implementing cybersecurity recommendations (3A-NI-08) https://www.csteachers.org/page/standards
- Compare ways software developers protect devices and information from unauthorized access (3B-NI-04) https://www.csteachers.org/page/standards
- Explain security issues that might lead to compromised computer programs (3B-AP-18) https://www.csteachers.org/page/standards

## Resources
- https://en.wikipedia.org/wiki/API_key
- https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0

Copyright &copy; 2025 Knight Moves. All Rights Reserved.
