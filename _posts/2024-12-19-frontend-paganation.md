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
  <div class="card">
    <nz-card>
      <div class="ng-Header col-xs-12">
        <i nz-icon nzType="unordered-list" nzTheme="outline"></i>
        Search 
      </div>
      <div class="searchboxAerar pt-4">
        <form
          nz-form
          [formGroup]="searchForm"
          class="ant-advanced-search-form"
          (ngSubmit)="submitSearchForm()"
          style="padding: 24px; background-color: #fbfbfb; border: 1px solid #d9d9d9; border-radius: 6px;"
        >
          <div class="form-row">
            <div class="form-group col-md-4">
              <div class="col-md-12">
                <nz-form-label>Agreement Type</nz-form-label>
                <nz-form-item>
                  <nz-form-control>
                    <nz-select 
                      nzShowSearch 
                      nzAllowClear 
                      formControlName="agreementTypeId" 
                      nzPlaceHolder="Select Agreement Type"
                    >
                      <nz-option
                        *ngFor="let agreetype of agreementType"
                        [nzLabel]="agreetype.agreementType"
                        [nzValue]="agreetype.id"
                      >
                      </nz-option>
                    </nz-select>
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>

            <div class="form-group col-md-4">
              <div class="col-md-12">
                <nz-form-label>Name of Organization</nz-form-label>
                <nz-form-item>
                  <nz-form-control>
                    <input
                      nz-input
                      type="text"
                      formControlName="nameOfOrganization"
                      placeholder="Enter organization name"
                    />
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>

            <div class="form-group col-md-4">
              <div class="col-md-12">
                <nz-form-label>Country Name</nz-form-label>
                <nz-form-item>
                  <nz-form-control>
                    <nz-select
                      nzShowSearch
                      nzAllowClear
                      formControlName="countryId"
                      nzPlaceHolder="Select Country"
                    >
                      <nz-option
                        *ngFor="let country of countries"
                        [nzLabel]="country.country"
                        [nzValue]="country.id"
                      >
                      </nz-option>
                    </nz-select>
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>

            <div class="form-group col-md-4">
              <div class="col-md-12">
                <nz-form-label>Subject</nz-form-label>
                <nz-form-item>
                  <nz-form-control>
                    <input
                      nz-input
                      type="text"
                      formControlName="subjectEnglish"
                      placeholder="Enter subject"
                    />
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>

            <div class="col-md-4">
              <nz-form-label style="margin-left: 15px">Signing Date From</nz-form-label>
              <div class="col-md-12">
                <nz-form-item>
                  <nz-form-control
                    [nzSpan]="null"
                    nzHasFeedback
                    nz-col
                    nzErrorTip="Please insert valid Date"
                  >
                    <nz-date-picker
                      formControlName="signingDateFrom"
                      placeholder="From Date"
                      style="width: 100%"
                      [nzDisabledDate]="disabledFutureDate"
                    >
                    </nz-date-picker>
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>

            <div class="col-md-4">
              <nz-form-label style="margin-left: 15px">Signing Date To</nz-form-label>
              <div class="col-md-12">
                <nz-form-item>
                  <nz-form-control
                    [nzSpan]="null"
                    nzHasFeedback
                    nz-col
                    nzErrorTip="Please insert valid Date"
                  >
                    <nz-date-picker
                      formControlName="signingDateTo"
                      placeholder="To Date"
                      style="width: 100%"
                      [nzDisabledDate]="disabledPastDate"
                    >
                    </nz-date-picker>
                  </nz-form-control>
                </nz-form-item>
              </div>
            </div>
          </div>
        </form>

        <div class="d-flex flex-row-reverse">
          <div class="p-2">
            <button class="btn-dark ant-btn" (click)="onDownloadReport()">
              <span class="ng-star-inserted">Download Report</span>
            </button>
          </div>
          <div class="p-2">
            <button class="ant-btn" (click)="onRefresh()">
              <span class="ng-star-inserted">Refresh Data</span>
            </button>
          </div>
          <div class="p-2">
            <button nz-button [nzType]="'primary'" (click)="submitSearchForm()">Search</button>
          </div>
        </div>
      </div>
    </nz-card>
  </div>
</nz-card>
```

### Component Class
```typescript
import { Component } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';
import { MraStorageService } from 'src/app/modules/mra/services/mra-storage.service';
import { MRA } from 'src/app/modules/mra/components/model/mra.model';
import { NzNotificationService } from 'ng-zorro-antd/notification';
import { Country } from 'src/app/modules/mra/components/model/country.model';
import { DatePipe } from '@angular/common';
import { ServerResponse } from 'src/app/shared/models/dto/server-response.dto';
import { CountryService } from 'src/app/modules/mra/services/country.service';
import { NzTableQueryParams } from 'ng-zorro-antd/table';
import { applicationPermissions } from 'src/app/shared/application-constants/application-permissions';
import { ExcelDownloadService } from 'src/app/shared/services/excel-download.service';
import { differenceInCalendarDays, setHours } from 'date-fns';

@Component({
  selector: 'app-mra-list-admin',
  templateUrl: './mra-list-admin.component.html',
  styleUrls: ['./mra-list-admin.component.scss'],
})
export class MraListAdminComponent {
  searchForm: FormGroup;
  agreementType: any;
  accessTypeList: any;
  mraList: MRA[] = [];
  countries: Country[] = [];
  applicationPermissions = applicationPermissions;

  total: number = 0;
  size: number = 10;
  page: number = 1;

  sortingKey: string = 'date_of_signature';
  sortingValue: string = 'descend';

  constructor(
    private fb: FormBuilder,
    private mraStorageService: MraStorageService,
    private countryService: CountryService,
    private notification: NzNotificationService,
    private excelExport: ExcelDownloadService
  ) {
    this.searchForm = this.fb.group({
      agreementTypeId: [null],
      nameOfOrganization: [null],
      countryId: [null],
      subjectEnglish: [null],
      signingDateFrom: [null],
      signingDateTo: [null],
    });
  }

  today: Date = new Date();

  ngOnInit(): void {
    this.loadCountries();
    this.loadAgreementType();
    this.loadAccessType();
    this.loadDatasFromServer();
  }

  loadCountries(): void {
    this.countryService.getCountriesAll().subscribe(
      (data) => {
        this.countries = data;
      },
      (error) => {
        console.error('Error fetching countries:', error);
      }
    );
  }

  loadAgreementType(): void {
    this.countryService.getAllAgreementType().subscribe(
      (data) => {
        this.agreementType = data;
      },
      (error) => {
        console.error('Error fetching agreementType:', error);
      }
    );
  }

  loadAccessType(): void {
    this.mraStorageService.getAllAccessType().subscribe(
      (data) => {
        this.accessTypeList = data;
      },
      (error) => {
        console.error('Error fetching accessType:', error);
      }
    );
  }

  submitSearchForm() {
    var pipe = new DatePipe('en-US');
    if (this.searchForm.controls.signingDateFrom.value) {
      const generalFromDateFormat = pipe.transform(
        this.searchForm.controls.signingDateFrom.value,
        'yyyy-MM-dd 00:00'
      );
      this.searchForm.controls.signingDateFrom.setValue(generalFromDateFormat);
    }
    if (this.searchForm.controls.signingDateTo.value) {
      const generalToDateFormat = pipe.transform(
        this.searchForm.controls.signingDateTo.value,
        'yyyy-MM-dd 23:59'
      );
      this.searchForm.controls.signingDateTo.setValue(generalToDateFormat);
    }
    console.log(this.searchForm);
    this.page = 1;
    this.size = 10;
    this.loadDatasFromServer();
  }

  onRefresh() {
    this.searchForm?.reset();
    this.submitSearchForm();
  }

  loadDatasFromServer(): void {
    this.mraStorageService
      .searchMra(
        this.searchForm.value,
        this.page,
        this.size,
        this.sortingKey,
        this.sortingValue
      )
      .subscribe({
        next: (res: ServerResponse) => {
          if (res?.success && res?.data) {
            this.mraList = res?.data?.content;
            this.total = res?.data?.totalElements;
          } else {
            this.mraList = [];
            this.notification.warning(
              'Warning !',
              'No data found for the given search parameters !'
            );
          }
        },
        error: (error) => {
          this.mraList = [];

          if (error.status === 0) {
            this.notification.error(
              'Error',
              'Network issue, please check your connection.'
            );
          } else if (error.status >= 500) {
            this.notification.error(
              'Error',
              'Server error, please try again later.'
            );
          } else if (error.status >= 400) {
            this.notification.error(
              'Error',
              'Invalid request, please check your inputs.'
            );
          } else {
            this.notification.error('Error', 'An unexpected error occurred.');
          }
        },
        complete: () => {},
      });
  }

  onQueryParamsChange(params: NzTableQueryParams): void {
    this.page = params.pageIndex;
    this.size = params.pageSize;

    params.sort.forEach((element) => {
      if (element.value != null) {
        this.sortingKey = element.key;
        this.sortingValue = element.value;
      }
    });

    this.loadDatasFromServer();
  }

  deleteMra(id: number, agreementType: any): void {
    this.mraStorageService.deleteMra(id).subscribe({
      next: (response: ServerResponse) => {
        if(response){
        if (response.success === true) {
          this.notification.success(
            'Success !',
            agreementType + ' has been deleted successfully !'
          );
          this.loadDatasFromServer();
        } else if (response.success === false) {
          this.notification.error(
            'Failed !',
            agreementType + ' Can not be deleted!'
          );
        }
      } else {
        this.notification.error(
          'Failed !',
          agreementType + ' deleted Failed!'
        );
      }

      },
      error: (error) => {
        if (error.status === 0) {
          this.notification.error(
            'Error',
            'Network issue, please check your connection.'
          );
        } else if (error.status >= 500) {
          this.notification.error(
            'Error',
            'Server error, please try again later.'
          );
        } else if (error.status >= 400) {
          this.notification.error(
            'Error',
            'Invalid request, please check your inputs.'
          );
        } else {
          this.notification.error('Error', 'An unexpected error occurred.');
        }
      },

    });
  }

  onDownloadReport() {
    this.mraStorageService.getMraReport(this.searchForm.value).subscribe(
      (res) => {
        if (res?.data === null || res?.data?.length === 0) {
          this.notification.warning(
            'Warning!',
            'No data available to download'
          );
        } else {
          const dataList = this.getFormatDataForExcel(res?.data);
          this.excelExport.exportExcelV2(dataList, 'List of MRA/MOU');
        }
      },
      (error) => {
        this.notification.error('Error!', 'Excel Sheet Data fetch Failed');
      }
    );
  }

  getFormatDataForExcel(dataReport: any) {
    const reportMap = new Map();
    const dataList = [];
    let i = 1;
    for (const data of dataReport) {
      reportMap.set('#SL', i);
      reportMap.set('Agreement Type', data.agreementType);
      reportMap.set('Subject', data.subjectEnglish);
      reportMap.set('Name of Organization', data.nameOfOrganizationEnglish);
      reportMap.set('Country Name', data.country);
      reportMap.set(
        'Date Of Signature',
        data.dateOfSignature ? new Date(data.dateOfSignature) : null
      );

      const jsonObject: any = {};
      reportMap.forEach((value, key) => {
        jsonObject[key] = value;
      });

      dataList.push(jsonObject);
      i++;
    }

    return dataList;
  }
  disabledPastDate = (current: Date): boolean =>
    differenceInCalendarDays(current, this.today) < 0;

  disabledFutureDate = (current: Date): boolean =>
    differenceInCalendarDays(current, this.today) > 0;
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
import { HttpClient, HttpErrorResponse, HttpParams } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { catchError, map } from 'rxjs/operators';
import { applicationUrls } from 'src/app/shared/application-constants/application-urls.const';
import { ServerResponse } from 'src/app/shared/models/dto/server-response.dto';
import { MRA } from 'src/app/modules/mra/components/model/mra.model';
import { Country } from 'src/app/modules/mra/components/model/country.model';
import { AgreementType } from 'src/app/modules/mra/components/model/agreementType.model';
import { HttpErrorHandler } from 'src/app/shared/services/customhttp-error-handler';
import { MraInfoSearch } from 'src/app/modules/mra/components/model/mra-info-search';
import { Attachments } from 'src/app/modules/mra/components/model/attachment.model';
import { DomSanitizer, SafeUrl } from '@angular/platform-browser';
import { MraSearchDto } from '../components/model/mra.search.model';
import { MRAInfoSearch } from '../models/DTO/mra-info-search';
import { Attachment } from '../models/DTO/public-view-dto';
import { AccessType } from '../../policy-guidelines/components/documents/models/DTO/document-dto';
import { PaginatedResponse } from 'src/app/modules/mra/components/model/paginated-response.model';

@Injectable({
  providedIn: 'root',
})
export class MraStorageService {
  private apiUrlforAllMra = `${applicationUrls.pgDocument.getAllMra}`;
  private apiUrlforAddMra = `${applicationUrls.pgDocument.addMra}`;
  private apiUrlforDeleteMra= `${applicationUrls.pgDocument.deleteMra}`;
  private apiUrlforSearchMra= `${applicationUrls.pgDocument.searchMra}`;
  private apiUrlforMraReport= `${applicationUrls.pgDocument.getMraReport}`;
  private apiUrlforEditMra= `${applicationUrls.pgDocument.editMra}`;
  private apiGetMraById= `${applicationUrls.pgDocument.getMraById}`;
  private apiGetAttachmentByMraId= `${applicationUrls.pgDocument.getAttachmentByMraId}`;
  private apiGetPublicAttachmentByMraId= `${applicationUrls.pgDocument.getPublicAttachmentByMraId}`;
  private apiGetAttachmentFileByMraId= `${applicationUrls.pgDocument.getAttachmentFileByMraId}`;
  private apiUrlforAddAgreemantType = `${applicationUrls.pgDocument.addAgreementType}`;
  private apiUrlAgrementTypeByMraId = `${applicationUrls.pgDocument.getAgreementTypeByMraId}`;
  private apiUrlCountryByMraId = `${applicationUrls.pgDocument.getCountryByMraId}`;
  private apiUrlForAccessType = `${applicationUrls.pgDocument.getAllAccessType}`;
  private apiUrlForAgreementTypeSortedList = `${applicationUrls.pgDocument.getAllAgreementTypeWithSorting}`;
  private apiUrlForAgreementTypeDelete = `${applicationUrls.pgDocument.deleteAgreementType}`;
  private apiUrlForAgreementTypeEdit = `${applicationUrls.pgDocument.editAgreementType}`;
  private apiUrlForDeleteAttachment = `${applicationUrls.pgDocument.deleteAttachment}`;

  private handleError: <T>(operation?: string, result?: T) => (error: HttpErrorResponse) => Observable<T>;

  previewUrl: SafeUrl | null = null;

  constructor(
    private httpClient: HttpClient,
    private sanitizer: DomSanitizer,
    private customErrorHandler: HttpErrorHandler
  ) {
    this.handleError = customErrorHandler.createErrorHandler('MRAService');
  }

  saveMRA(newMra: MRA): Observable<MRA> {
    return this.httpClient.post<MRA>(this.apiUrlforAddMra, newMra).pipe(
      catchError(this.handleError<MRA>('saveMra')) // Use correct type for error handling
    );

