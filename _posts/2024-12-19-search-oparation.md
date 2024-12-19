---
layout: post
title: search Form for Country
subtitle: search Form for country 
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [REST, angular, paganation,Java,Spring Boot]
comments: true
mathjax: false
author: Noor
---

# **search frontend **  

## 1. **search Form**

 <nz-card>
    <div class="ng-Header col-xs-12">
      <i nz-icon nzType="unordered-list" nzTheme="outline"></i>
      Searce 
    </div>
    <div class="searchboxAerar pt-4">

      <form
  nz-form
  [formGroup]="searchForm"
  class="ant-advanced-search-form"
  (ngSubmit)="submitSearchForm()"
  style="
    padding: 24px;
    background-color: #fbfbfb;
    border: 1px solid #d9d9d9;
    border-radius: 6px;
  "
>
        <div class="form-row">
          <div class="form-group col-md-4">
            <div class="col-md-12">
              <nz-form-label>Agreement Type</nz-form-label>
              <nz-form-item>
                <nz-form-control>
                  <nz-select nzShowSearch nzAllowClear formControlName="agreementTypeId" nzPlaceHolder="Select Agreement Type">
                    <nz-option
                    *ngFor="let agreetype of agreementType"
                    [nzLabel]="agreetype.agreementType"
                    [nzValue]="agreetype.id">
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
            <nz-form-label style="margin-left: 15px"
              >Signing Date From</nz-form-label
            >
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
            <nz-form-label style="margin-left: 15px"
              >Signing Date To</nz-form-label
            >
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
              <span class="ng-star-inserted"> Download Report </span>
            </button>
          </div>
          <div class="p-2">
            <button class="ant-btn" (click)="onRefresh()">
              <span class="ng-star-inserted">Refresh Data</span>
            </button>
          </div>
          <div class="p-2">
            <button nz-button [nzType]="'primary'" (click)="submitSearchForm()" >Search</button>
          </div>
        </div>
    </div>
  </nz-card>

  ## 2. **search Form Angular**

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

 ## 3. **search dto Angular**
export class MraInfoSearch {
  public agreementType: string;
  public organizationName: string;
  public countryName: string;
  public accessType: string; 
  public signingDataFrom: string;
  public signingDataTo: string;
  public size: number;
  public page: number;
  public sortingKey: string;
  public sortingValue: string;
  public disabled: boolean = false;
    constructor() {}
}

 ## 4. **search SERVICE Angular**

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
  }

  saveAgreementType(newAgreementType: AgreementType): Observable<AgreementType> {
    return this.httpClient.post<AgreementType>(this.apiUrlforAddAgreemantType, newAgreementType).pipe(
      catchError(this.handleError<AgreementType>('saveMra')) // Use correct type for error handling
    );
  }
  getAgreementTypewithSorting(page: number, size: number, sortingKey: string, sortingValue: string): Observable<PaginatedResponse<AgreementType>> {
    return this.httpClient.get<PaginatedResponse<AgreementType>>(`${this.apiUrlForAgreementTypeSortedList}`, {
      params: {
        page: page.toString(),
        size: size.toString(),
        sortingKey: sortingKey,
        sortingValue: sortingValue
      }
    }).pipe(
      catchError(this.handleError<PaginatedResponse<AgreementType>>('getAgreementType', { items: [], totalCount: 0 }))
    );
  }

  deleteAttachment(id:number, attachment: string): Observable<ServerResponse> {
    const params = {
      id: id,
      attachmentTitle: attachment,
    };
      return this.httpClient.post<ServerResponse>(`${this.apiUrlForDeleteAttachment}`, params);
  }

  deleteAgreementType(id: number): Observable<void> {
    return this.httpClient.delete<void>(`${this.apiUrlForAgreementTypeDelete}/${id}`).pipe(
      catchError(this.handleError<void>('deleteAgreementType'))
    );
  }
  updateAgreementType(id: number, agreementTypeData: AgreementType): Observable<AgreementType> {
    return this.httpClient.put<AgreementType>(`${this.apiUrlForAgreementTypeEdit}/${id}`, agreementTypeData).pipe(
      catchError(this.handleError<AgreementType>('save Agreement Type')) // Use correct type for error handling
    );
  }

  updateMra(id: number, mraData: MRA): Observable<MRA> {
    return this.httpClient.post<MRA>(`${this.apiUrlforEditMra}/${id}`, mraData).pipe(
      catchError(this.handleError<MRA>('saveMra')) // Use correct type for error handling
    );
  }
  getMra(): Observable<MRA[]> {
    return this.httpClient.get<MRA[]>(this.apiUrlforAllMra).pipe(
      map((response) => response as MRA[]), // Cast response to Country[]
      catchError(this.handleError<MRA[]>('getMRA', [])) // Provide an empty array as a fallback
    );
  }

  deleteMra(id: number): Observable<ServerResponse> {
    return this.httpClient.delete<ServerResponse>(`${this.apiUrlforDeleteMra}/${id}`).pipe(
      catchError(this.handleError<ServerResponse>('deleteMra'))
    );
  }

  searchMra(filters: any, page: number, size: number, sortingKey?: string, sortingValue?: string): Observable<any> {
    const params = {
      page: page - 1,
      size: size,
      sortingKey: sortingKey ? sortingKey : null,
      sortingValue: sortingValue ? sortingValue : null,
      agreementTypeId: filters.agreementTypeId,
      nameOfOrganization: filters.nameOfOrganization,
      countryId: filters.countryId,
      subjectEnglish: filters.subjectEnglish,
      signingDateFrom: filters.signingDateFrom,
      signingDateTo: filters.signingDateTo
    };
      return this.httpClient.post<ServerResponse>(`${this.apiUrlforSearchMra}`, params);
  }

  getMraReport(filters: any): Observable<any> {
    const params = {
      agreementTypeId: filters.agreementTypeId,
      nameOfOrganization: filters.nameOfOrganization,
      countryId: filters.countryId,
      accessTypeId: filters.accessTypeId,
      signingDateFrom: filters.signingDateFrom,
      signingDateTo: filters.signingDateTo
    };

    return this.httpClient.post<ServerResponse>(`${this.apiUrlforMraReport}`, params);
  }

  getMraById(id: number): Observable<MRA> {
    return this.httpClient.get<MRA>(`${this.apiGetMraById}/${id}`).pipe(
      catchError(this.handleError<MRA>('getMraById'))
    );
  }

  getAttachmentByMraId(id: number): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(
        `${this.apiGetAttachmentByMraId}` + id
      )
      .pipe(
        map((serverResponse: ServerResponse) => {
          if (!serverResponse.data) {
            return null;
          }
          return serverResponse;
        })
      );
  }

  getPublicAttachmentByMraId(id: number): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(
        `${this.apiGetPublicAttachmentByMraId}` + id
      )
      .pipe(
        map((serverResponse: ServerResponse) => {
          if (!serverResponse.data) {
            return null;
          }
          return serverResponse;
        })
      );
  }

  getCountryByMraId(id: number):  Observable<Country> {
    return this.httpClient.get<Country>(`${this.apiUrlCountryByMraId}/${id}`).pipe(
      map((response) => response as Country), // Cast response to Country[]
      catchError(this.handleError<Country>('Country')) // Provide an empty array as a fallback
    );
  }



  getAgreementTypeByMraId(id: number):  Observable<AgreementType> {
    return this.httpClient.get<AgreementType>(`${this.apiUrlAgrementTypeByMraId}/${id}`).pipe(
      map((response) => response as AgreementType), // Cast response to Country[]
      catchError(this.handleError<AgreementType>('AgreementType')) // Provide an empty array as a fallback
    );
  }

  getAttachmentFileByMraId(id: number):  Observable<String[]> {
    return this.httpClient.get<String[]>(`${this.apiGetAttachmentFileByMraId}/${id}`).pipe(
      map((response) => response as String[]), // Cast response to Country[]
      catchError(this.handleError<String[]>('getMRAAttachment', [])) // Provide an empty array as a fallback
    );
  }

  fetchAndPreviewAttachment(filePath: string): void {
    this.httpClient.get(`api/attachments/${filePath}`, { responseType: 'blob' }).subscribe(
      (response) => {
        const objectURL = URL.createObjectURL(response);
        this.previewUrl = this.sanitizer.bypassSecurityTrustUrl(objectURL);
      },
      (error) => {
        console.error("Error fetching file preview:", error);
      }
    );
  }

  //#region read cs count
  readCSCount(): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(`${applicationUrls.mra.readCSCount}`)
      .pipe(
        map((serverResponse: ServerResponse) => {
          return serverResponse.data;
        })
      );
  }
  //#endregion

  //#region read cs count
  readCADCount(): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(`${applicationUrls.mra.readCADCount}`)
      .pipe(
        map((serverResponse: ServerResponse) => {
          return serverResponse.data;
        })
      );
  }
  //#endregion

  //#region read cs count
  readCBLMCount(): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(`${applicationUrls.mra.readCBLMCount}`)
      .pipe(
        map((serverResponse: ServerResponse) => {
          return serverResponse.data;
        })
      );
  }
  //#endregion

  //#region read mra description
  readMraDescription(): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(`${applicationUrls.mra.readMraDescription}`)
      .pipe(
        map((serverResponse: ServerResponse) => {
          return serverResponse.data;
        })
      );
  }
  //#endregion

  //#region read mra description
  readRssFeedData(): Observable<any> {
    return this.httpClient
      .get<ServerResponse>(`${applicationUrls.mra.readRssFeedData}`)
      .pipe(
        map((serverResponse: ServerResponse) => {
          return serverResponse.data;
        })
      );
  }
  //#endregion

  readMraPublicInfo(
      mraInfoSearch: MRAInfoSearch
    ): Observable<ServerResponse> {
      mraInfoSearch.disabled = false;
      return this.httpClient.post<ServerResponse>(
        `${applicationUrls.pgDocument.readMraListPublic}`,
        mraInfoSearch
      );
  }

  getAllAccessType(): Observable<AccessType[]> {
    return this.httpClient.get<AccessType[]>(this.apiUrlForAccessType).pipe(
      map((response) => response as AccessType[]), // Cast response to AccessType[]
      catchError(this.handleError<AccessType[]>('AgreementType', [])) // Provide an empty array as a fallback
    );
  }

  saveMraInfo(
    mraInfo: any,
  ): Observable<ServerResponse> {
    return this.httpClient.post<ServerResponse>(
      `${applicationUrls.mra.saveMraInfo}`,
      mraInfo
    );
  }

  updateMraInfo(
    mraInfo: any,
    mraId: number | null,
  ): Observable<ServerResponse> {
    return this.httpClient.put<ServerResponse>(
      `${applicationUrls.mra.updateMraInfo}/` +
      mraId,
        mraInfo
    );
  }

  getMRAInfoById(
      id: number
    ): Observable<ServerResponse> {
      const params = new HttpParams().append(
        'id',
        `${id}`
      );
      return this.httpClient.get<ServerResponse>(
        `${applicationUrls.mra.getMraInfoById}`,
        { params }
      );
    }
}

 ## 5. **search REST API Angular**
searchMra: environment.pgApiUrl + 'mra/search',

 ## 6. ** Paganation Angular**
 <nz-card>
    <div class="ng-Header col-xs-12">
      <i nz-icon nzType="unordered-list" nzTheme="outline"></i>
      {{ " List of MRA/MOU " }}
    </div>
    <div nz-col [nzSpan]="24">

      <nz-table
        #basicTableForAdminListInfo
        [nzData]="mraList"
        nzTableLayout="fixed"
        nzShowSizeChanger
        nzBordered
        nzSize="middle"
        nzAlign="middle"
        [nzFrontPagination]="false"
        [nzTotal]="total"
        [(nzPageSize)]="size"
        [nzShowTotal]="totalRowRangeTemplate"
        [(nzPageIndex)]="page"
        (nzQueryParams)="onQueryParamsChange($event)"
        [nzPaginationPosition]="'both'"
        [nzScroll]="{ x: '1100px' }"
      >
        <ng-template
          #totalRowRangeTemplate
          let-range="range"
          let-total
          style="text-align: left"
        >
          <div style="text-align: left">
            Showing {{ range[0] }}-{{ range[1] }} of {{ total }} items
          </div>
        </ng-template>
        <thead>
          <tr>
            <th style="width: 50px; text-align: center" rowspan="1">SI.</th>
            <th
              style="text-align: center"
              rowspan="1"
              nzColumnKey="ag.agreement_type"
              [nzSortFn]="true"
            >
              Agreement Type
            </th>
            <th
              style="text-align: center"
              rowspan="1"
              nzColumnKey="subject_english"
              [nzSortFn]="true"
            >
              Subject
            </th>
            <th
              style="text-align: center"
              rowspan="1"
              nzColumnKey="name_of_organization_english"
              [nzSortFn]="true"
            >
              Name of Organization
            </th>
            <th
              style="text-align: center"
              rowspan="1"
              nzColumnKey="c.country"
              [nzSortFn]="true"
            >
              Country Name
            </th>
            <th
              style="text-align: center"
              rowspan="1"
              nzColumnKey="date_of_signature"
              [nzSortFn]="true"
            >
              Date Of Signature
            </th>
            <th style="width: 15%; text-align: center">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let data of mraList; let i = index">
            <td style="text-align: center">
              {{ (page - 1) * size + 1 + i }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.agreementType }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.subjectEnglish }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.nameOfOrganizationEnglish }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.country }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.dateOfSignature | date : "dd-MM-yyyy" }}
            </td>
            <td style="width: 15%; text-align: center">
              <a
                class="ml-2 mt-2"
                nz-tooltip
                nzTooltipTitle="View in Details"
                nzTooltipPlacement="bottomLeft"
                nz-button
                nzType="primary"
                [routerLink]="['/home/mra/view-mra']"
                [queryParams]="{ id: data.id }"
                type="submit"
                routerLinkActive="router-link-active"
                target="_blank"
                style="margin: 1%"
              >
                <i nz-icon nzType="eye" nzTheme="outline"></i>
              </a>
              <a [appRequiredPermission]="applicationPermissions.mra.mraEditPermission"
                nz-button
                nzType="primary"
                [routerLink]="['/home/mra/edit-mra']"
                [queryParams]="{ id: data.id }"
                type="submit"
                routerLinkActive="router-link-active"
                target="_blank"
                style="margin: 1%"
                nz-tooltip
                nzTooltipPlacement="bottomLeft"
              >
                <i nz-icon nzType="edit" nzTheme="outline"></i>
              </a>
              <a [appRequiredPermission]="applicationPermissions.mra.mraDeletePermission"
                nz-button
                nzType="danger"
                nz-popconfirm
                nzPopconfirmTitle="Are you sure to delete this item?"
                nzTooltipPlacement="bottomLeft"
                (nzOnConfirm)="deleteMra(data.id, data.agreementType)"
                style="margin: 1%"
              >
                <i nz-icon nzType="delete" nzTheme="outline"></i>
              </a>
            </td>
          </tr>
        </tbody>
      </nz-table>
    </div>
  </nz-card>

 ## 7. **search REST API Spring boot**
     @PostMapping("/searrch")
    public ResponseEntity<?> searchList(@RequestBody MraRequestDto mraDto) throws Exception {
            ApiResponse response = Service.search(mraDto);
            return ResponseEntity.ok(response);
    }
 ## 7. **search REST Service Spring boot**
 {: .box-success}
  public ApiResponse searchMRA(RequestDto pageRequest) throws Exception {
        try {
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern(formatPattern);
            Pageable pageable;

            PageableRequestDTO pageRequestDTO = new PageableRequestDTO();
            PageableRequestDTO pageSettings = new PageableRequestDTO() {{
                setPage(0);
                setSize(DEFAULT_PAGE_SIZE);
            }};

            if (pageRequest != null && pageRequest.getPage() != null && pageRequest.getSize() != null) {
                pageRequestDTO.setPage(pageRequest.getPage());
                pageRequestDTO.setSize(pageRequest.getSize());
                pageRequestDTO.setSortingKey(pageRequest.getSortingKey());
                pageRequestDTO.setSortingValue(pageRequest.getSortingValue());
                pageSettings = pageRequestDTO;
            }

            Sort.Direction sortingValue = null;
            if ("descend".equals(pageRequest.getSortingValue())) {
                sortingValue = Sort.Direction.DESC;
            } else {
                sortingValue = Sort.Direction.ASC;
            }

            if (pageRequest.getSortingKey() != null) {
                pageable = PageRequest.of(pageSettings.getPage(), pageSettings.getSize(), Sort.by(sortingValue, pageRequest.getSortingKey()));
            } else {
                pageable = PageRequest.of(pageSettings.getPage(), pageSettings.getSize());
            }
            int agreementTypeIdSearch = 0;
            int accessTypeIdSearch = 0;
            int countryIdSearch = 0;
            int nameOfOrganizationSearch = 0;
            int signingDateStartSearch = 0;
            int signingDateEndSearch = 0;
            String nameOfOrganization = null;
            String subjectEnglish = null;
            int subjectEnglishSearch = 0;

            if (Objects.isNull(pageRequest.getAgreementTypeId())) {
                agreementTypeIdSearch = 1;
                pageRequest.setAgreementTypeId(1L);
            }


            if (Objects.isNull(pageRequest.getCountryId())) {
                countryIdSearch = 1;
                pageRequest.setCountryId(1L);
            }

            if (StringUtils.isNotEmpty(pageRequest.getNameOfOrganization())) {
                nameOfOrganization = pageRequest.getNameOfOrganization().toLowerCase();
            } else {
                nameOfOrganizationSearch = 1;
            }

            if (StringUtils.isNotEmpty(pageRequest.getSubjectEnglish())) {
                subjectEnglish = pageRequest.getSubjectEnglish().toLowerCase();
            } else {
                subjectEnglishSearch = 1;
            }

            LocalDateTime signingDateEnd = LocalDateTime.now();
            LocalDateTime signingDateStart = LocalDateTime.now();

            if (StringUtils.isEmpty(pageRequest.getSigningDateFrom())) {
                signingDateStartSearch = 1;
                pageRequest.setSigningDateFrom(String.valueOf(LocalDateTime.now()));
            } else {
                try {
                    signingDateStart = LocalDateTime.parse(pageRequest.getSigningDateFrom(), formatter);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }

            if (StringUtils.isEmpty(pageRequest.getSigningDateTo())) {
                signingDateEndSearch = 1;
                pageRequest.setSigningDateTo(String.valueOf(LocalDateTime.now()));
            } else {
                try {
                    signingDateEnd = LocalDateTime.parse(pageRequest.getSigningDateTo(), formatter);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }

            try {
                Page<MraDto> mraInfo = mraRepository.findAllMra(
                        pageable,
                        agreementTypeIdSearch, pageRequest.getAgreementTypeId(),
                        nameOfOrganizationSearch, nameOfOrganization,
                        countryIdSearch, pageRequest.getCountryId(),
                        subjectEnglishSearch, pageRequest.getSubjectEnglish(),
                        signingDateStartSearch, signingDateStart,
                        signingDateEndSearch, signingDateEnd
                );
                return new ApiResponse(true, "Success", mraInfo);
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
        } catch (Exception ex) {
            ex.printStackTrace();
            return new ApiResponse(false, "Could not get mra info because " + ex.getMessage());
        }
    }

    public ApiResponse getReport(RequestDto mraDto) {
        try {
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern(formatPattern);

            int agreementTypeIdSearch = 0;
            int accessTypeIdSearch = 0;
            int countryIdSearch = 0;
            int nameOfOrganizationSearch = 0;
            int signingDateStartSearch = 0;
            int signingDateEndSearch = 0;
            String nameOfOrganization = null;

            if (Objects.isNull(mraDto.getAgreementTypeId())) {
                agreementTypeIdSearch = 1;
                mraDto.setAgreementTypeId(1L);
            }

            if (Objects.isNull(mraDto.getAccessTypeId())) {
                accessTypeIdSearch = 1;
                mraDto.setAccessTypeId(1L);
            }

            if (Objects.isNull(mraDto.getCountryId())) {
                countryIdSearch = 1;
                mraDto.setCountryId(1L);
            }

            if (StringUtils.isNotEmpty(mraDto.getNameOfOrganization())) {
                nameOfOrganization = mraDto.getNameOfOrganization().toLowerCase();
            } else {
                nameOfOrganizationSearch = 1;
            }

            LocalDateTime signingDateEnd = LocalDateTime.now();
            LocalDateTime signingDateStart = LocalDateTime.now();

            if (StringUtils.isEmpty(mraDto.getSigningDateFrom())) {
                signingDateStartSearch = 1;
                mraDto.setSigningDateFrom(String.valueOf(LocalDateTime.now()));
            } else {
                try {
                    signingDateStart = LocalDateTime.parse(mraDto.getSigningDateFrom(), formatter);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }

            if (StringUtils.isEmpty(mraDto.getSigningDateTo())) {
                signingDateEndSearch = 1;
                mraDto.setSigningDateTo(String.valueOf(LocalDateTime.now()));
            } else {
                try {
                    signingDateEnd = LocalDateTime.parse(mraDto.getSigningDateTo(), formatter);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }

            List<MraDto> mraDtoList = mraRepository.getMraReport(
                    agreementTypeIdSearch, mraDto.getAgreementTypeId(),
                    nameOfOrganizationSearch, nameOfOrganization,
                    countryIdSearch, mraDto.getCountryId(),
                    accessTypeIdSearch, mraDto.getAccessTypeId(),
                    signingDateStartSearch, signingDateStart,
                    signingDateEndSearch, signingDateEnd
            );

            return new ApiResponse(true, "Success", mraDtoList);
        } catch (Exception ex) {
            ex.printStackTrace();
            return new ApiResponse(false, "Could not get mra report because " + ex.getMessage());
        }
    }


 ## 7. **search REST DTO Spring boot**

    public class RequestDto {
    private Long agreementTypeId;
    private String nameOfOrganization;
    private String subjectEnglish;
    private Long countryId;
    private Long accessTypeId;
    private String signingDateFrom;
    private String signingDateTo;
    private String signatureDate;
    private Integer size;
    private Integer page;
    private String sortingKey;
    private String sortingValue;
}

 ## 7. **search REST Repository Spring boot**
@Query(value = "SELECT DISTINCT m.id as id, " +
            "ag.agreement_type as agreementType, " +
            "m.subject_english as subjectEnglish, " +
            "m.name_of_organization_english as nameOfOrganizationEnglish , " +
            "m.date_of_signature as dateOfSignature, " +
            "c.country as country " +
            "FROM mra m " +
            "LEFT JOIN country c ON m.country_id = c.id " +
            "LEFT JOIN attachment a ON m.id = a.mra_id " +
            "LEFT JOIN agreement_type ag ON m.agreement_type_id = ag.id " +
            "WHERE (1 = :agreementTypeIdSearch OR m.agreement_type_id = :agreementTypeId) " +
            "AND (1 = :nameOfOrganizationSearch OR LOWER(m.name_of_organization_english) LIKE CONCAT('%', CAST(:nameOfOrganization AS text), '%')) " +
            "AND (1 = :countryIdSearch OR m.country_id = :countryId) " +
            "AND (1 = :subjectEnglishSearch OR LOWER(m.subject_english) LIKE CONCAT('%', CAST(:subjectEnglishh AS text), '%')) " +
            "AND (1 = :signingDateStartSearch OR CAST(m.date_of_signature AS DATE) >= CAST(:signingStartDate AS DATE)) " +
            "AND (1 = :signingDateEndSearch OR CAST(m.date_of_signature AS DATE) <= CAST(:signingEndDate AS DATE)) ", nativeQuery = true)
    Page<Dto> findAllMra(Pageable pageable,
                            @Param("agreementTypeIdSearch") int agreementTypeIdSearch,
                            @Param("agreementTypeId") Long agreementTypeId,
                            @Param("nameOfOrganizationSearch") int nameOfOrganizationSearch,
                            @Param("nameOfOrganization") String nameOfOrganization,
                            @Param("countryIdSearch") int countryIdSearch,
                            @Param("countryId") Long countryId,
                            @Param("subjectEnglishSearch") int subjectEnglishSearch,
                            @Param("subjectEnglishh") String subjectEnglishh,
                            @Param("signingDateStartSearch") int signingDateStartSearch,
                            @Param("signingStartDate") LocalDateTime signingStartDate,
                            @Param("signingDateEndSearch") int signingDateEndSearch,
                            @Param("signingEndDate") LocalDateTime signingEndDate
    );

 ## 8. **Thank you**