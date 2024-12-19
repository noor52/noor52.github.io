---
layout: post
title: Search Form for Country
subtitle: Search Form Implementation with Angular and Spring Boot
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [REST, Angular, Pagination, Java, Spring Boot]
comments: true
mathjax: false
author: Noor
---

# Search Form Implementation Guide

## 1. Frontend Components

### HTML Template
```html
<nz-card>
  <div class="ng-Header col-xs-12">
    <i nz-icon nzType="unordered-list" nzTheme="outline"></i>
    Search
  </div>
  <!-- Search form implementation -->
</nz-card>
```

### Component Class
```typescript
@Component({
  selector: 'app-mra-list-admin',
  templateUrl: './mra-list-admin.component.html'
})
export class MraListAdminComponent {
  // Component implementation
}
```

## 2. Data Models

```typescript
export class MraInfoSearch {
  public agreementType: string;
  public organizationName: string;
  public countryName: string;
  // Other properties
}
```

## 3. Services

```typescript
@Injectable({
  providedIn: 'root'
})
export class MraStorageService {
  // Service implementation
}
```

## 4. Backend Implementation

### Controller
```java
@PostMapping("/search")
public ResponseEntity<?> searchList(@RequestBody MraRequestDto mraDto) {
    ApiResponse response = service.search(mraDto);
    return ResponseEntity.ok(response);
}
```

### Service Layer
```java
public ApiResponse searchMRA(RequestDto pageRequest) {
    // Service implementation
}
```

### Repository
```java
@Query(value = """
    SELECT DISTINCT m.id as id, 
           ag.agreement_type as agreementType
    FROM mra m 
    LEFT JOIN country c ON m.country_id = c.id 
    WHERE // conditions
""", nativeQuery = true)
Page<MraDto> findAllMra(Pageable pageable, /* parameters */);
```

## 5. Pagination Implementation

```html
<nz-table #basicTableForAdminListInfo [nzData]="mraList">
  <!-- Table implementation -->
</nz-table>
```