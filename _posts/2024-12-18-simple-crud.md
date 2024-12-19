---
layout: post
title: CRUD Operation for Country
subtitle: REST CRUD for country
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [java, REST, angular, spring-boot, crud]
comments: true
mathjax: false
author: Noor
---

# CRUD Operation for Country in Spring Boot  

In modern software development, building a REST API for managing data is a crucial task. In this post, we will explore how to perform CRUD (Create, Read, Update, Delete) operations for a `Country` resource using **Spring Boot**.

Here’s how we can implement a simple CRUD REST API for managing countries:

## 1. **Create rest API of Country**  

To create a country, you need to send a `POST` request with the country details in the request body. Here's how you can do that:

```java
2. Add Countries
@PostMapping("/add-country")
public ResponseEntity<ApiResponse> saveCountry(@RequestBody CountryDto country) {
    ApiResponse savedCountry = countryService.addCountry(country);
    return new ResponseEntity<>(savedCountry, HttpStatus.OK);
}

2. Read (Get) All Countries
To retrieve all countries, we use the GET request. It supports pagination and sorting by various keys.

@GetMapping("/get-all-countries")
public ResponseEntity<PaginatedResponse<Country>> getAllCountries(
        @RequestParam(defaultValue = "1") int page,
        @RequestParam(defaultValue = "10") int size,
        @RequestParam(required = false) String sortingKey,
        @RequestParam(required = false) String sortingValue) {

    // Call the service to get paginated countries
    PaginatedResponse<Country> response = countryService.getAllCountries(page, size, sortingKey, sortingValue);
    return ResponseEntity.ok(response);
}

3. Update a Country
To update an existing country, you can send a PUT request with the updated country data.

@PutMapping("/edit-country/{id}")
public ResponseEntity<ApiResponse> editCountry(@PathVariable("id") Long id, @RequestBody CountryDto updatedCountry) {
    ApiResponse response = countryService.updateCountry(updatedCountry, id);
    return new ResponseEntity<>(response, HttpStatus.OK);
}

4. Delete a Country
To delete a country, send a DELETE request with the country’s id.

@DeleteMapping("/delete-country/{id}")
public ResponseEntity<ApiResponse> deleteCountry(@PathVariable("id") Long id) {
    ApiResponse response = countryService.removeCountry(id);
    return new ResponseEntity<>(response, HttpStatus.OK);
}
```