---
layout: post
title: search Form for Country
subtitle: search Form for country 
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [REST, angular, form,Java,Spring Boot]
comments: true
mathjax: false
author: Noor
---

# **Create Angular frontend **  

## 1. **Create Form**

 <div class="card">
  <div class="ng-Header col-xs-12">
    <i nz-icon nzType="form" nzTheme="outline"></i>
    {{ isEditMode ? "Update MRA/MOU" : "Create MRA/MOU" }}
  </div>
  <div class="searchboxAerar pt-4">
    <form nz-form [formGroup]="mraMouForm" (ngSubmit)="submitForm()">
      <div class="form-row">
        <div class="form-group col-md-4">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label nzRequired>Agreement Type</nz-form-label>
              </div>
              <!-- <div>
                <button
                  type="button"
                  class="btn btn-warning d-flex"
                  (click)="showModal()"
                  nz-tooltip
                  nzTooltipTitle="Add New Research Type"
                  nzTooltipPlacement="topLeft"
                >
                  <i nz-icon nzType="plus" nzTheme="outline"></i>
                </button>
              </div> -->
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="rtNameErrorTpl">
                <nz-select nzShowSearch nzAllowClear formControlName="agreementTypeId" nzPlaceHolder="Select type">
                  <nz-option *ngFor="let at of agreementTypeList" [nzValue]="at.id" [nzLabel]="at.agreementType">
                  </nz-option>
                </nz-select>
                <ng-template #rtNameErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select type !
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>
        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Subject (English)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="subjectEnglishErrorTpl">
                <input nz-input type="text" id="subjectEnglish" formControlName="subjectEnglish"
                  placeholder="Enter subject in English" />
              </nz-form-control>
            </nz-form-item>
            <!-- Error Template for Subject English -->
            <ng-template #subjectEnglishErrorTpl let-control>
              <ng-container *ngIf="control.hasError('required')">
                Insert subject english please !
              </ng-container>
              <ng-container *ngIf="control.hasError('pattern')">
                Only English letters are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>
        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Subject (Bangla)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="subjectBanglaErrorTpl">
                <input nz-input type="text" id="subjectBangla" formControlName="subjectBangla"
                  placeholder="Enter subject in Bangla" />
              </nz-form-control>
            </nz-form-item>
            <ng-template #subjectBanglaErrorTpl let-control>
              <ng-container *ngIf="control.hasError('pattern')">
                Only Bangla letters are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Introduction (English)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="introductionEnglishErrorTpl">
                <input nz-input type="text" id="introductionEnglish" formControlName="introductionEnglish"
                  placeholder="Enter introduction in English" />
              </nz-form-control>
            </nz-form-item>
            <ng-template #introductionEnglishErrorTpl let-control>
              <ng-container *ngIf="control.hasError('pattern')">
                Only English letters are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Introduction (Bangla)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="introductionBanglaErrorTpl">
                <input nz-input type="text" id="introductionBangla" formControlName="introductionBangla"
                  placeholder="Enter introduction in Bangla" />
              </nz-form-control>
            </nz-form-item>
            <ng-template #introductionBanglaErrorTpl let-control>
              <ng-container *ngIf="control.hasError('pattern')">
                Only Bangla letters are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Name of organization (English)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="nameOfOrganizationEnglishErrorTpl">
                <input nz-input type="text" id="nameOfOrganizationEnglish" formControlName="nameOfOrganizationEnglish"
                  placeholder="Enter organization in English" />
              </nz-form-control>
            </nz-form-item>
            <ng-template #nameOfOrganizationEnglishErrorTpl let-control>
              <ng-container *ngIf="control.hasError('organizationError')">
                Either Subject [English] or Subject [Bangla] is required.
              </ng-container>
              <ng-container *ngIf="control.hasError('pattern')">
                Only English letters are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Name of organization (Bangla)</nz-form-label>
            <nz-form-item>
              <nz-form-control nzHasFeedback [nzErrorTip]="nameOfOrganizationBanglaErrorTpl">
                <input nz-input type="text" id="nameOfOrganizationBangla" formControlName="nameOfOrganizationBangla"
                  placeholder="Enter organization in Bangla" />
              </nz-form-control>
            </nz-form-item>
            <ng-template #nameOfOrganizationBanglaErrorTpl let-control>
              <ng-container *ngIf="control.hasError('organizationError')">
                Either Subject [English] or Subject [Bangla] is required.
              </ng-container>
              <ng-container *ngIf="control.hasError('pattern')">
                Only Bangla letter are allowed.
              </ng-container>
            </ng-template>
          </div>
        </div>
        <div class="form-group col-md-4">
          <nz-form-label nzRequired style="margin-left: 15px">Signing Date</nz-form-label>
          <div class="col-md-12">
            <nz-form-item>
              <nz-form-control [nzSpan]="null" nzHasFeedback nz-col [nzErrorTip]="dateOfSignatureErrorTpl">
                <nz-date-picker formControlName="dateOfSignature" placeholder="Date of Signature" style="width: 100%"
                  nzFormat="dd-MM-yyyy" [nzDisabledDate]="disabledDate">
                </nz-date-picker>
              </nz-form-control>
              <ng-template #dateOfSignatureErrorTpl let-control>
                <ng-container *ngIf="control.hasError('required')">
                  Please select valid date!
                </ng-container>
              </ng-template>
            </nz-form-item>
          </div>
        </div>
        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Country Name</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="countryId" id="countryId" nzPlaceHolder="Select country" nzShowSearch
                  [nzFilterOption]="filterOption">
                  <nz-option *ngFor="let country of countryList" [nzLabel]="country.country" [nzValue]="country.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>
        <!-- Attachment 1 -->
        <div class="form-group col-md-5">
          <div class="col-md-12">
            <nz-form-label nzRequired>Attachment Title - 1</nz-form-label>
            <textarea rows="1" nz-input id="attachmentTitle1" formControlName="attachmentTitle1"
              placeholder="Insert attachment title 1"></textarea>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label nzRequired>Access Type - 1</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="accessType1" id="accessType1" nzPlaceHolder="Select Access Type"
                  nzShowSearch nzAllowClear required>
                  <nz-option *ngFor="let aType of accessTypeList" [nzLabel]="aType.accessTypeName" [nzValue]="aType.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="form-group col-md-3">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label nzRequired>Attachment - 1</nz-form-label>
              </div>
              <div *ngIf="fileShowForAttachment1">
                <button style="margin-right: 5px;" nz-button primary type="button" nzType="primary" nz-tooltip
                  nzTooltipTitle="Attachment one Preview" nzTooltipPlacement="topLeft"
                  (click)="setBase64AttachmentForPreview('attachment1')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div style="margin-right: 5px;" *ngIf="!fileShowForAttachment1 && filePreviewForAttachment1">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment one Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64Attachment1ForPreview('attachment1')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div *ngIf="deleteAttachment1">
                <button nz-button type="button" nzType="danger" nz-popconfirm
                  nzPopconfirmTitle="Are you sure to delete this item?" nzTooltipPlacement="bottomLeft"
                  (nzOnConfirm)="onCancelAttachment1()">
                  <i nz-icon nzType="delete"></i>
                </button>
              </div>
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback nzValidatingTip="Validating..." [nzErrorTip]="attachment1ErrorTpl">
                <input #myInput1 type="file" nz-input (change)="onSelectAttachment1($event)" nz-tooltip
                  nzTooltipTitle=".pdf/.doc/xlsx/image files are allowed. Maximum size 30 MB."
                  nzTooltipPlacement="bottomLeft" />
                <ng-template #attachment1ErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select a valid file!
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <!-- Attachment 2 -->
        <div class="form-group col-md-5">
          <div class="col-md-12">
            <nz-form-label>Attachment Title - 2</nz-form-label>
            <textarea rows="1" nz-input id="attachmentTitle2" formControlName="attachmentTitle2"
              placeholder="Insert attachment title 2"></textarea>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Access Type - 2</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="accessType2" id="accessType2" nzPlaceHolder="Select Access Type"
                  nzShowSearch nzAllowClear>
                  <nz-option *ngFor="let aType of accessTypeList" [nzLabel]="aType.accessTypeName" [nzValue]="aType.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="form-group col-md-3">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label>Attachment - 2</nz-form-label>
              </div>
              <div style="margin-right: 5px;" *ngIf="fileShowForAttachment2">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment two Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64AttachmentForPreview('attachment2')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div style="margin-right: 5px;" *ngIf="!fileShowForAttachment2 && filePreviewForAttachment2">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment tro Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64Attachment2ForPreview('attachment2')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div *ngIf="deleteAttachment2">
                <button nz-button type="button" nzType="danger" nz-popconfirm
                  nzPopconfirmTitle="Are you sure to delete this item?" nzTooltipPlacement="bottomLeft"
                  (nzOnConfirm)="onDeleteAttachment2()">
                  <i nz-icon nzType="delete"></i>
                </button>
              </div>
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback nzValidatingTip="Validating..." [nzErrorTip]="attachment2ErrorTpl">
                <input #myInput2 type="file" nz-input (change)="onSelectAttachment2($event)" nz-tooltip
                  nzTooltipTitle=".pdf/.doc/xlsx/image files are allowed. Maximum size 30 MB."
                  nzTooltipPlacement="bottomLeft" />
                <ng-template #attachment2ErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select Photo!
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <!-- Attachment 3 -->
        <div class="form-group col-md-5">
          <div class="col-md-12">
            <nz-form-label>Attachment Title - 3</nz-form-label>
            <textarea rows="1" nz-input id="attachmentTitle3" formControlName="attachmentTitle3"
              placeholder="Insert attachment title 3"></textarea>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Access Type - 3</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="accessType3" id="accessType3" nzPlaceHolder="Select Access Type"
                  nzShowSearch nzAllowClear>
                  <nz-option *ngFor="let aType of accessTypeList" [nzLabel]="aType.accessTypeName" [nzValue]="aType.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="form-group col-md-3">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label>Attachment - 3</nz-form-label>
              </div>
              <div style="margin-right: 5px;" *ngIf="fileShowForAttachment3">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment three Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64AttachmentForPreview('attachment3')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div  style="margin-right: 5px;" *ngIf="!fileShowForAttachment3 && filePreviewForAttachment3">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment one Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64Attachment3ForPreview('attachment3')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div *ngIf="deleteAttachment3">
                <button nz-button type="button" nzType="danger" nz-popconfirm
                  nzPopconfirmTitle="Are you sure to delete this item?" nzTooltipPlacement="bottomLeft"
                  (nzOnConfirm)="onDeleteAttachment3()">
                  <i nz-icon nzType="delete"></i>
                </button>
              </div>
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback nzValidatingTip="Validating..." [nzErrorTip]="attachment3ErrorTpl">
                <input #myInput3 type="file" nz-input (change)="onSelectAttachment3($event)" nz-tooltip
                  nzTooltipTitle=".pdf/.doc/xlsx/image files are allowed. Maximum size 30 MB."
                  nzTooltipPlacement="bottomLeft" />
                <ng-template #attachment3ErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select Photo!
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <!-- Attachment 4 -->
        <div class="form-group col-md-5">
          <div class="col-md-12">
            <nz-form-label>Attachment Title - 4</nz-form-label>
            <textarea rows="1" nz-input id="attachmentTitle4" formControlName="attachmentTitle4"
              placeholder="Insert attachment title 4"></textarea>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Access Type - 4</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="accessType4" id="accessType4" nzPlaceHolder="Select Access Type"
                  nzShowSearch nzAllowClear>
                  <nz-option *ngFor="let aType of accessTypeList" [nzLabel]="aType.accessTypeName" [nzValue]="aType.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="form-group col-md-3">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label>Attachment - 4</nz-form-label>
              </div>
              <div  style="margin-right: 5px;"  *ngIf="fileShowForAttachment4">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment four Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64AttachmentForPreview('attachment4')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div style="margin-right: 5px;" *ngIf="!fileShowForAttachment4 && filePreviewForAttachment4">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment one Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64Attachment4ForPreview('attachment4')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div *ngIf="deleteAttachment4">
                <button nz-button type="button" nzType="danger" nz-popconfirm
                  nzPopconfirmTitle="Are you sure to delete this item?" nzTooltipPlacement="bottomLeft"
                  (nzOnConfirm)="onDeleteAttachment4()">
                  <i nz-icon nzType="delete"></i>
                </button>
              </div>
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback nzValidatingTip="Validating..." [nzErrorTip]="attachment3ErrorTpl">
                <input #myInput4 type="file" nz-input (change)="onSelectAttachment4($event)" nz-tooltip
                  nzTooltipTitle=".pdf/.doc/xlsx/image files are allowed. Maximum size 30 MB."
                  nzTooltipPlacement="bottomLeft" />
                <ng-template #attachment4ErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select Photo!
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <!-- Attachment 5 -->
        <div class="form-group col-md-5">
          <div class="col-md-12">
            <nz-form-label>Attachment Title - 5</nz-form-label>
            <textarea rows="1" nz-input id="attachmentTitle5" formControlName="attachmentTitle5"
              placeholder="Insert attachment title 5"></textarea>
          </div>
        </div>

        <div class="form-group col-md-4">
          <div class="col-md-12">
            <nz-form-label>Access Type - 5</nz-form-label>
            <nz-form-item>
              <nz-form-control>
                <nz-select formControlName="accessType5" id="accessType5" nzPlaceHolder="Select Access Type"
                  nzShowSearch nzAllowClear>
                  <nz-option *ngFor="let aType of accessTypeList" [nzLabel]="aType.accessTypeName" [nzValue]="aType.id">
                  </nz-option>
                </nz-select>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="form-group col-md-3">
          <div class="col-md-12">
            <div class="row">
              <div style="margin-left: 15px">
                <nz-form-label>Attachment - 5</nz-form-label>
              </div>
              <div  style="margin-right: 5px;" *ngIf="fileShowForAttachment5">
                <button nz-button type="button" nzType="primary" nzType="primary" nz-tooltip nzTooltipTitle="Attachment five Preview"
                nzTooltipPlacement="topLeft" (click)="setBase64AttachmentForPreview('attachment5')">
                <i nz-icon nzType="eye"></i>
              </button>
              </div>
              <div style="margin-right: 5px;" *ngIf="!fileShowForAttachment5 && filePreviewForAttachment5">
                <button nz-button type="button" nzType="primary" nz-tooltip nzTooltipTitle="Attachment one Preview"
                  nzTooltipPlacement="topLeft" (click)="setBase64Attachment5ForPreview('attachment5')">
                  <i nz-icon nzType="eye"></i>
                </button>
              </div>
              <div *ngIf="deleteAttachment5">
                <button nz-button type="button" nzType="danger" nz-popconfirm
                  nzPopconfirmTitle="Are you sure to delete this item?" nzTooltipPlacement="bottomLeft"
                  (nzOnConfirm)="onDeleteAttachment5()">
                  <i nz-icon nzType="delete"></i>
                </button>
              </div>
            </div>
            <nz-form-item>
              <nz-form-control nzHasFeedback nzValidatingTip="Validating..." [nzErrorTip]="attachment5ErrorTpl">
                <input #myInput5 type="file" nz-input (change)="onSelectAttachment5($event)" nz-tooltip
                  nzTooltipTitle=".pdf/.doc/xlsx/image files are allowed. Maximum size 30 MB."
                  nzTooltipPlacement="bottomLeft" />
                <ng-template #attachment5ErrorTpl let-control>
                  <ng-container *ngIf="control.hasError('required')">
                    Please select Photo!
                  </ng-container>
                </ng-template>
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>
      </div>
      <div class="col-md-12">
        <div class="row justify-content-center media-button pt-3">
          <div class="col-sm-5 col-md-2 col-xs-2 margin-bottom">
            <button nz-button type="submit" class="btn btn-success active btn-lg btn-block cari border-redius"
              [disabled]="!isAttachment1Uploaded || !mraMouForm.valid" [appRequiredPermission]="
                applicationPermissions.researchAndStudies
                  .addFormSaveButtonPermission
              ">
              <i nz-icon nzType="save" nzTheme="fill"></i>
              {{ isEditMode ? "Update" : "Save" }}
            </button>
          </div>
        </div>
      </div>
    </form>
  </div>
</div>

<nz-modal style="width: 800px" [(nzVisible)]="isVisible" nzTitle="Add Agreement Type" (nzOnCancel)="handleCancel()"
  (nzOnOk)="handleOk()">
  <ng-container *nzModalContent>
    <!-- Wrap the form content with the formGroup directive -->
    <div [formGroup]="agreementForm">
      <div nz-col [nzSpan]="24">
        <div class="row justify-content-center media-button mt-4">
          <div class="form-row">
            <div class="form-group col-md-12">
              <div class="col-md-12">
                <nz-form-label>Agreement Type</nz-form-label>
                <nz-form-item>
                  <nz-form-control>
                    <!-- Bind the input to the form control using formControlName -->
                    <input nz-input type="text" formControlName="newAgreementType" placeholder="Agreement Type" />
                  </nz-form-control>
                </nz-form-item>
              </div>

              <div class="col-xs-12 col-sm-12">
                <button type="submit" class="btn btn-success active btn-lg btn-block cari border-redius">
                  <i nz-icon nzType="save" nzTheme="fill"></i>
                  {{ isEditMode ? "Update" : "Submit" }}
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </ng-container>
</nz-modal>
<nz-modal [(nzVisible)]="isVisibleForAttachment" (nzOnCancel)="handlePreviewModalCancel()" [nzClosable]="false"
  [nzOkText]="null" [nzWidth]="1200">
  <ng-container *nzModalContent>
    <iframe *ngIf="!isImageLoading && pdfUrl" [src]="pdfUrl" style="width: 100%; height: 35vw"></iframe>
    <div style="text-align: center">
      <img class="img-thumbnail" *ngIf="imageURL" [src]="imageURL" /><br />
      <ng-template #noImageFound>
        <img src="https://gw.alipayobjects.com/zos/antfincdn/K%24NnlsB%26hz/pageHeader.svg" alt="Fallbackimage" />
      </ng-template>
    </div>
  </ng-container>
</nz-modal>

  ## 2. **search Form Angular**

 import { Component, ElementRef, OnInit, ViewChild } from '@angular/core';
import {
  FormArray,
  FormBuilder,
  FormGroup,
  Validators,
  ValidationErrors,
} from '@angular/forms';
import { applicationPermissions } from 'src/app/shared/application-constants/application-permissions';
import { AgreementType } from '../model/agreementType.model';
import { MraStorageService } from '../../services/mra-storage.service';
import { CountryService } from '../../services/country.service';
import { DomSanitizer, SafeUrl } from '@angular/platform-browser';
import { ActivatedRoute, Router } from '@angular/router';
import { NzNotificationService } from 'ng-zorro-antd/notification';
import { Country } from '../model/country.model';
import { AccessType } from '../../models/access-type.model';
import { MRAAttachment } from '../../models/DTO/mra-attachment';
import { UtilityService } from 'src/app/shared/services/utility.service';
import { environment } from 'src/environments/environment';
import { DatePipe } from '@angular/common';
import { ArgumentType } from '@angular/compiler/src/core';
import { differenceInCalendarDays, setHours } from 'date-fns';
import { NonFullScreenPageMode, values } from 'pdf-lib';
import { combineLatest } from 'rxjs';

@Component({
  selector: 'app-create-mra-mou',
  templateUrl: './create-mra-mou.component.html',
  styleUrls: ['./create-mra-mou.component.scss'],
})
export class CreateMraMouComponent implements OnInit {
  //#region value or variables
  mraMouForm: FormGroup;
  agreementForm: FormGroup;

  isEditMode: boolean = false;
  isVisible = false;
  mraId: any;
  mraInfo: any;

  today = new Date();

  agreementTypeList: AgreementType[] = [];
  countryList: Country[] = [];
  accessTypeList: AccessType[] = [];
  //#endregion

  //#region permission
  applicationPermissions = applicationPermissions;
  //#endregion

  deleteAttachment1: boolean = false;
  deleteAttachment2: boolean = false;
  deleteAttachment3: boolean = false;
  deleteAttachment4: boolean = false;
  deleteAttachment5: boolean = false;

  //#region photo file setup
  attachmentUrl1: any;
  attachmentUrl2: any;
  attachmentUrl3: any;
  attachmentUrl4: any;
  attachmentUrl5: any;
  allowedFileExtensions = '.png,.jpg,.jpeg,.docx,.doc,.xlsx,.pdf';
  imageTypeArray: string[] = ['jpg', 'png', 'jpeg'];
  maxFormatFileSize = 30;
  fileRequired: boolean = true;
  fileField: boolean = false;
  isImageLoading: boolean;
  imageURL: SafeUrl;
  otherPdfUrl: any;
  pdfUrl: any;
  @ViewChild('myInput1') myInputVariable1: ElementRef;
  @ViewChild('myInput2') myInputVariable2: ElementRef;
  @ViewChild('myInput3') myInputVariable3: ElementRef;
  @ViewChild('myInput4') myInputVariable4: ElementRef;
  @ViewChild('myInput5') myInputVariable5: ElementRef;
  previewAttachments: MRAAttachment[] = [];
  fileList: any[] = [];
  isFileUpload = false;
  saveBtnDisabled: boolean = false;
  isVisibleForAttachment = false;

  isAttachment1Uploaded: boolean = false;
  isAttachment2Uploaded: boolean = false;
  isAttachment3Uploaded: boolean = false;
  isAttachment4Uploaded: boolean = false;
  isAttachment5Uploaded: boolean = false;

  filePreviewForAttachment1: boolean = false;
  filePreviewForAttachment2: boolean = false;
  filePreviewForAttachment3: boolean = false;
  filePreviewForAttachment4: boolean = false;
  filePreviewForAttachment5: boolean = false;

  fileShowForAttachment1: boolean = false;
  fileShowForAttachment2: boolean = false;
  fileShowForAttachment3: boolean = false;
  fileShowForAttachment4: boolean = false;
  fileShowForAttachment5: boolean = false;

  attachmentId1: number;
  attachmentId2: number;
  attachmentId3: number;
  attachmentId4: number;
  attachmentId5: number;
  //#endregion

  //#region constructor
  constructor(
    private fb: FormBuilder,
    private mraStorageService: MraStorageService,
    private countryService: CountryService,
    private sanitizer: DomSanitizer,
    private activatedRoute: ActivatedRoute,
    private router: Router,
    private notification: NzNotificationService,
    private utilityService: UtilityService
  ) {
    const mraIdParam = Number(
      this.activatedRoute.snapshot.queryParamMap.get('id')
    );
    if (mraIdParam !== 0) {
      this.mraId = Number(mraIdParam);
    } else {
      this.mraId = null;
    } //#endregion
  }
  //#endregion
  disabledDate = (current: Date): boolean =>
    // Can not select days before today and today
    differenceInCalendarDays(current, this.today) > 0;

  //#region fetch agreement type list
  loadAgreementType(): void {
    this.countryService.getAllAgreementType().subscribe(
      (data) => {
        this.agreementTypeList = data;
      },
      (error) => {
        console.error('Error fetching agreementType:', error);
      }
    );
  }
  //#endregion

  //#region fetch country list
  loadCountries(): void {
    this.countryService.getCountriesAll().subscribe(
      (data) => {
        this.countryList = data;
      },
      (error) => {
        console.error('Error fetching countries:', error);
      }
    );
  }
  //#endregion

  //#region access type list
  loadAccessType(): void {
    this.mraStorageService.getAllAccessType().subscribe(
      (data) => {
        this.accessTypeList = data;
      },
      (error) => {
        console.error('Error fetching agreementType:', error);
      }
    );
  }
  //#endregion

  //#region modal functionality
  showModal(): void {
    this.isVisible = true;
  }

  handleCancel(): void {
    this.isVisible = false;
  }

  handleOk(): void {
    this.isVisible = false;
    // Additional actions on modal confirmation, if necessary
  }
  //#endregion

  //#region on init
  ngOnInit(): void {
    this.loadAccessType();
    this.formInit();
    this.loadAgreementType();
    this.loadCountries();
    this.getDetailsInfoById();
  }
  //#endregion

  //#region form initialization
  formInit() {
    this.mraMouForm = this.fb.group({
      agreementTypeId: ['', Validators.required],
      subjectEnglish: ['', Validators.pattern(/^(?!\s*$)[a-zA-Z\s]*$/)],
      subjectBangla: ['', Validators.pattern(/^(?!\s*$)[\u0980-\u09FF\s]+$/)], // Bangla-only validatio
      introductionEnglish: ['', Validators.pattern(/^(?!\s*$)[a-zA-Z\s]*$/)],
      introductionBangla: [
        '',
        Validators.pattern(/^(?!\s*$)[\u0980-\u09FF\s]+$/),
      ],
      nameOfOrganizationEnglish: [
        '',
        Validators.pattern(/^(?!\s*$)[a-zA-Z\s]*$/),
      ], // English-only validation
      nameOfOrganizationBangla: [
        '',
        Validators.pattern(/^(?!\s*$)[\u0980-\u09FF\s]+$/),
      ], // Bangla-only validation
      dateOfSignature: ['', Validators.required],
      countryId: [''],

      attachmentTitle1: ['', Validators.required],
      accessType1: [2, Validators.required],
      attachment1: [''],

      attachmentTitle2: [''],
      accessType2: [2],
      attachment2: [''],

      attachmentTitle3: [''],
      accessType3: [2],
      attachment3: [''],

      attachmentTitle4: [''],
      accessType4: [2],
      attachment4: [''],

      attachmentTitle5: [''],
      accessType5: [2],
      attachment5: [''],
    });

    this.agreementForm = this.fb.group({
      newAgreementType: [
        '',
        [Validators.required, Validators.pattern(/^\S+$/)],
      ],
    });
    this.mraMouForm
      .get('introductionBangla')
      ?.valueChanges.subscribe((value) => {
        if (value) {
          const subjectEnglishValue =
            this.mraMouForm.get('subjectEnglish')?.value;
          const subjectBanglaValue =
            this.mraMouForm.get('subjectBangla')?.value;

          if (
            subjectEnglishValue === null ||
            subjectEnglishValue === '' ||
            subjectEnglishValue === undefined
          ) {
            if (
              subjectBanglaValue === null ||
              subjectBanglaValue === '' ||
              subjectBanglaValue === undefined
            ) {
              this.notification.warning(
                'Required!',
                'Enter Subject English or Bangla'
              );
            }
          }
        }
      });

    this.mraMouForm
      .get('introductionEnglish')
      ?.valueChanges.subscribe((value) => {
        if (value) {
          const subjectEnglishValue =
            this.mraMouForm.get('subjectEnglish')?.value;
          const subjectBanglaValue =
            this.mraMouForm.get('subjectBangla')?.value;

          if (
            subjectEnglishValue === null ||
            subjectEnglishValue === '' ||
            subjectEnglishValue === undefined
          ) {
            if (
              subjectBanglaValue === null ||
              subjectBanglaValue === '' ||
              subjectBanglaValue === undefined
            ) {
              this.notification.warning(
                'Required!',
                'Enter Subject English or Bangla'
              );
            }
          }
        }
      });
    this.mraMouForm
      .get('nameOfOrganizationEnglish')
      ?.valueChanges.subscribe((value) => {
        if (value) {
          const subjectEnglishValue =
            this.mraMouForm.get('subjectEnglish')?.value;
          const subjectBanglaValue =
            this.mraMouForm.get('subjectBangla')?.value;

          if (
            subjectEnglishValue === null ||
            subjectEnglishValue === '' ||
            subjectEnglishValue === undefined
          ) {
            if (
              subjectBanglaValue === null ||
              subjectBanglaValue === '' ||
              subjectBanglaValue === undefined
            ) {
              this.notification.warning(
                'Required!',
                'Enter Subject English or Bangla'
              );
            }
          }
        }
      });

    this.mraMouForm
      .get('nameOfOrganizationBangla')
      ?.valueChanges.subscribe((value) => {
        if (value) {
          const subjectEnglishValue =
            this.mraMouForm.get('subjectEnglish')?.value;
          const subjectBanglaValue =
            this.mraMouForm.get('subjectBangla')?.value;

          if (
            subjectEnglishValue === null ||
            subjectEnglishValue === '' ||
            subjectEnglishValue === undefined
          ) {
            if (
              subjectBanglaValue === null ||
              subjectBanglaValue === '' ||
              subjectBanglaValue === undefined
            ) {
              this.notification.warning(
                'Required!',
                'Enter Subject English or Bangla'
              );
            }
          }
        }
      });

    this.mraMouForm.get('dateOfSignature')?.valueChanges.subscribe((value) => {
      if (value) {
        const nameOfOrganizationEnglishValue = this.mraMouForm.get(
          'nameOfOrganizationEnglish'
        )?.value;
        const nameOfOrganizationBanglaValue = this.mraMouForm.get(
          'nameOfOrganizationBangla'
        )?.value;

        if (
          nameOfOrganizationEnglishValue === null ||
          nameOfOrganizationEnglishValue === '' ||
          nameOfOrganizationEnglishValue === undefined
        ) {
          if (
            nameOfOrganizationBanglaValue === null ||
            nameOfOrganizationBanglaValue === '' ||
            nameOfOrganizationBanglaValue === undefined
          ) {
            this.notification.warning(
              'Required!',
              'Enter Name Of Organization English or Bangla'
            );
          }
        }
      }
    });

    this.mraMouForm.get('countryId')?.valueChanges.subscribe((value) => {
      if (value) {
        const nameOfOrganizationEnglishValue = this.mraMouForm.get(
          'nameOfOrganizationEnglish'
        )?.value;
        const nameOfOrganizationBanglaValue = this.mraMouForm.get(
          'nameOfOrganizationBangla'
        )?.value;

        if (
          nameOfOrganizationEnglishValue === null ||
          nameOfOrganizationEnglishValue === '' ||
          nameOfOrganizationEnglishValue === undefined
        ) {
          if (
            nameOfOrganizationBanglaValue === null ||
            nameOfOrganizationBanglaValue === '' ||
            nameOfOrganizationBanglaValue === undefined
          ) {
            this.notification.warning(
              'Required!',
              'Enter Name Of Organization English or Bangla'
            );
          }
        }
      }
    });

    this.mraMouForm.get('attachmentTitle3')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachmenttitle2 = this.mraMouForm.get('attachmentTitle2')?.value;
        if (
          attachmenttitle2 === null ||
          attachmenttitle2 === '' ||
          attachmenttitle2 === undefined
        ) {
          this.notification.warning('Required!', 'Enter attachmen 2 first');
        }
      }
    });
    this.mraMouForm.get('attachmentTitle4')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachmenttitle3 = this.mraMouForm.get('attachmentTitle3')?.value;
        if (
          attachmenttitle3 === null ||
          attachmenttitle3 === '' ||
          attachmenttitle3 === undefined
        ) {
          this.notification.warning('Required!', 'Enter attachmen 3 first');
        }
      }
    });

    this.mraMouForm.get('attachmentTitle5')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachmenttitle4 = this.mraMouForm.get('attachmentTitle4')?.value;
        if (
          attachmenttitle4 === null ||
          attachmenttitle4 === '' ||
          attachmenttitle4 === undefined
        ) {
          this.notification.warning('Required!', 'Enter attachmen 4 first');
        }
      }
    });

    this.mraMouForm.get('attachment3')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachment2 = this.mraMouForm.get('attachment2')?.value;
        const attachmenttitle2 = this.mraMouForm.get('attachmentTitle2')?.value;
        if ((
          attachment2 === null ||
          attachment2 === '' ||
          attachment2 === undefined )&&(
          attachmenttitle2 === null ||
          attachmenttitle2 === '' ||
          attachmenttitle2 === undefined
        )){
          this.notification.warning('Required!', 'Enter attachmen 2 first');
        }
      }
    });

    this.mraMouForm.get('attachment4')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachment3 = this.mraMouForm.get('attachment3')?.value;
        const attachmenttitle3 = this.mraMouForm.get('attachmentTitle3')?.value;
        if ((
          attachment3 === null ||
          attachment3 === '' ||
          attachment3 === undefined )&&(
          attachmenttitle3 === null ||
          attachmenttitle3 === '' ||
          attachmenttitle3 === undefined

        )) {
          this.notification.warning('Required!', 'Enter attachmen 3 first');
        }
      }
    });

    this.mraMouForm.get('attachment5')?.valueChanges.subscribe((value) => {
      if (value) {
        const attachment4 = this.mraMouForm.get('attachment4')?.value;
        const attachmenttitle4 = this.mraMouForm.get('attachmentTitle4')?.value;
        if ((
          attachment4 === null ||
          attachment4 === '' ||
          attachment4 === undefined )&&(
          attachmenttitle4 === null ||
          attachmenttitle4 === '' ||
          attachmenttitle4 === undefined
        )) {
          this.notification.warning('Required!', 'Enter attachmen 4 first');
        }
      }
    });

    this.mraMouForm.get('attachment1')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment1 = true;
      }
    });
    this.mraMouForm.get('attachmentTitle1')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment1 = true;
      }
    });

    this.mraMouForm.get('attachment2')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment2 = true;
      }
    });
    this.mraMouForm.get('attachmentTitle2')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment2 = true;
      }
    });
    this.mraMouForm.get('attachment3')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment3 = true;
      }
    });
    this.mraMouForm.get('attachmentTitle3')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment3 = true;
      }
    });

    this.mraMouForm.get('attachment4')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment4 = true;
      }
    });
    this.mraMouForm.get('attachmentTitle4')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment4 = true;
      }
    });

    this.mraMouForm.get('attachment5')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment5 = true;
      }
    });
    this.mraMouForm.get('attachmentTitle5')?.valueChanges.subscribe((value) => {
      if (value) {
        this.deleteAttachment5 = true;
      }
    });
  }

  //#endregion

  //#region handleAgreementTypeSubmit
  // handleAgreementTypeSubmit(): void {
  //   if (this.agreementForm.valid) {
  //     // Get the value from the form control
  //     const agreementType = this.agreementForm.value.newAgreementType.trim();

  //     // Call the service to save the data
  //     this.mraStorageService.saveAgreementType({ agreementType }).subscribe({
  //       next: () => {
  //         this.notification.success(
  //           'Success!',
  //           'Agreement Type information Saved Successfully'
  //         );
  //         this.agreementForm.reset();
  //         this.loadAgreementType();
  //         this.isVisible = false; // Close the modal after saving
  //       },
  //       error: (err) => {
  //         this.notification.warning(
  //           'Failed!',
  //           'AgreementType  information Save failes'
  //         );
  //         this.agreementForm.reset();
  //         console.error(err);
  //       },
  //     });
  //   } else {
  //     this.notification.warning(
  //       'Failed!',
  //       'Please enter a valid Agreement Type'
  //     );
  //   }
  // }
  //#endregion

  //#region submit form
  submitForm(): void {
    this.filePreviewForAttachment1 = false;
    this.filePreviewForAttachment2 = false;
    this.filePreviewForAttachment3 = false;
    this.filePreviewForAttachment4 = false;
    this.filePreviewForAttachment5 = false;
    var pipe = new DatePipe('en-US');
    const dateOfSignatureFormatted = pipe.transform(
      this.mraMouForm.controls.dateOfSignature.value,
      'yyyy-MM-dd HH:mm'
    );
    this.mraMouForm.controls.dateOfSignature.setValue(dateOfSignatureFormatted);
    const formData = new FormData();
    formData.append(
      'agreementTypeId',
      this.mraMouForm.controls.agreementTypeId.value
    );
    if (this.mraMouForm.controls.subjectEnglish.value) {
      formData.append(
        'subjectEnglish',
        this.mraMouForm.controls.subjectEnglish.value
      );
    }
    if (this.mraMouForm.controls.subjectBangla.value) {
      formData.append(
        'subjectBangla',
        this.mraMouForm.controls.subjectBangla.value
      );
    }
    if (this.mraMouForm.controls.introductionEnglish.value) {
      formData.append(
        'introductionEnglish',
        this.mraMouForm.controls.introductionEnglish.value
      );
    }
    if (this.mraMouForm.controls.introductionBangla.value) {
      formData.append(
        'introductionBangla',
        this.mraMouForm.controls.introductionBangla.value
      );
    }
    if (this.mraMouForm.controls.nameOfOrganizationEnglish.value) {
      formData.append(
        'nameOfOrganizationEnglish',
        this.mraMouForm.controls.nameOfOrganizationEnglish.value
      );
    }
    if (this.mraMouForm.controls.nameOfOrganizationBangla.value) {
      formData.append(
        'nameOfOrganizationBangla',
        this.mraMouForm.controls.nameOfOrganizationBangla.value
      );
    }
    if (this.mraMouForm.controls.countryId.value) {
      formData.append('countryId', this.mraMouForm.controls.countryId.value);
    }
    formData.append(
      'dateOfSignature',
      this.mraMouForm.controls.dateOfSignature?.value
    );
    if (
      this.mraMouForm.controls.attachment1.value ||
      this.attachmentUrl1 !== null
    ) {
      formData.append(
        'attachment1',
        this.mraMouForm.controls.attachment1.value
      );
      if (this.attachmentId1) {
        formData.append('attachmentId1', this.attachmentId1.toString());
      }
      formData.append(
        'attachmentTitle1',
        this.mraMouForm.controls.attachmentTitle1.value
      );
      formData.append(
        'accessType1',
        this.mraMouForm.controls.accessType1.value
      );
    } else {
      this.notification.warning(
        'Warning!!! ',
        'No documents have been uploaded by you! Please upload a document first.'
      );
    }

    if (
      this.mraMouForm.controls.attachmentTitle2.value &&
      this.mraMouForm.controls.accessType2.value &&
      (this.attachmentUrl2 != null ||
        this.mraMouForm.controls.attachment2.value)
    ) {
      formData.append(
        'attachment2',
        this.mraMouForm.controls.attachment2.value
      );
      if (this.attachmentId2) {
        formData.append('attachmentId2', this.attachmentId2.toString());
      }
      formData.append(
        'attachmentTitle2',
        this.mraMouForm.controls.attachmentTitle2.value
      );
      formData.append(
        'accessType2',
        this.mraMouForm.controls.accessType2.value
      );
    } else if (
      (this.mraMouForm.controls.attachmentTitle2.value &&
        !this.attachmentUrl2 &&
        !this.mraMouForm.controls.attachment2.value) ||
      (!this.mraMouForm.controls.attachmentTitle2.value &&
        (this.attachmentUrl2 || this.mraMouForm.controls.attachment2.value))
    ) {
      this.notification.warning(
        'Warning!!!',
        'Please complete all fields in Attachment 2 before submitting.'
      );
      return;
    }

    if (
      this.mraMouForm.controls.attachmentTitle3.value &&
      this.mraMouForm.controls.accessType3.value &&
      (this.attachmentUrl3 != null ||
        this.mraMouForm.controls.attachment3.value)
    ) {
      formData.append(
        'attachment3',
        this.mraMouForm.controls.attachment3.value
      );
      if (this.attachmentId3) {
        formData.append('attachmentId3', this.attachmentId3.toString());
      }
      formData.append(
        'attachmentTitle3',
        this.mraMouForm.controls.attachmentTitle3.value
      );
      formData.append(
        'accessType3',
        this.mraMouForm.controls.accessType3.value
      );
    } else if (
      (this.mraMouForm.controls.attachmentTitle3.value &&
        !this.attachmentUrl3 &&
        !this.mraMouForm.controls.attachment3.value) ||
      (!this.mraMouForm.controls.attachmentTitle3.value &&
        (this.attachmentUrl3 || this.mraMouForm.controls.attachment3.value))
    ) {
      this.notification.warning(
        'Warning!!!',
        'Please complete all fields in Attachment 3 before submitting.'
      );
      return;
    }

    if (
      this.mraMouForm.controls.attachmentTitle4.value &&
      this.mraMouForm.controls.accessType4.value &&
      (this.attachmentUrl4 != null ||
        this.mraMouForm.controls.attachment4.value)
    ) {
      formData.append(
        'attachment4',
        this.mraMouForm.controls.attachment4.value
      );
      if (this.attachmentId4) {
        formData.append('attachmentId4', this.attachmentId4.toString());
      }
      formData.append(
        'attachmentTitle4',
        this.mraMouForm.controls.attachmentTitle4.value
      );
      formData.append(
        'accessType4',
        this.mraMouForm.controls.accessType4.value
      );
    } else if (
      (this.mraMouForm.controls.attachmentTitle4.value &&
        !this.attachmentUrl4 &&
        !this.mraMouForm.controls.attachment4.value) ||
      (!this.mraMouForm.controls.attachmentTitle4.value &&
        (this.attachmentUrl4 || this.mraMouForm.controls.attachment4.value))
    ) {
      this.notification.warning(
        'Warning!!!',
        'Please complete all fields in Attachment 4 before submitting.'
      );
      return;
    }

    if (
      this.mraMouForm.controls.attachmentTitle5.value &&
      this.mraMouForm.controls.accessType5.value &&
      (this.attachmentUrl5 != null ||
        this.mraMouForm.controls.attachment5.value)
    ) {
      formData.append(
        'attachment5',
        this.mraMouForm.controls.attachment5.value
      );
      if (this.attachmentId5) {
        formData.append('attachmentId5', this.attachmentId5.toString());
      }
      formData.append(
        'attachmentTitle5',
        this.mraMouForm.controls.attachmentTitle5.value
      );
      formData.append(
        'accessType5',
        this.mraMouForm.controls.accessType5.value
      );
    } else if (
      (this.mraMouForm.controls.attachmentTitle5.value &&
        !this.attachmentUrl5 &&
        !this.mraMouForm.controls.attachment5.value) ||
      (!this.mraMouForm.controls.attachmentTitle5.value &&
        (this.attachmentUrl5 || this.mraMouForm.controls.attachment5.value))
    ) {
      this.notification.warning(
        'Warning!!!',
        'Please complete all fields in Attachment 5 before submitting.'
      );
      return;
    }

    if (this.isEditMode && this.mraId != null) {
      this.mraStorageService.updateMraInfo(formData, this.mraId).subscribe({
        next: (response: any) => {
          window.location.reload();
          if (response.success == true) {
            this.mraInfo = response?.data;
            this.notification.success('Success!', response.message);
            this.mraId = response?.data?.id;
            this.isEditMode = true;
            this.getDetailsInfoById();
          } else {
            this.notification.error(
              'Failed!',
              'MRA/MOU Update Failed',
              response.message
            );
            if (response.data?.documentUrl) {
              this.fileShowForAttachment1 = true;
            } else {
              this.fileShowForAttachment1 = false;
            }
          }
        },
        error: (error) => {
          this.notification.warning(
            'Failed!',
            'MRA/MOU Update Failed, ',
            error.error.message
          );
        },
      });
    } else {
      this.mraStorageService.saveMraInfo(formData).subscribe({
        next: (res: any) => {
          window.location.reload();
          if (res.success == true) {
            this.mraInfo = res?.data;
            this.mraId = res?.data?.id;
            this.notification.success('Success!', res.message);
            this.isEditMode = true;
            this.getDetailsInfoById();
          } else if (res.success == false) {
            this.notification.error('Failed!', res.message);
          } else {
            this.notification.error(
              'Failed!',
              'MRA/MOU saved Failed',
              res.message
            );
          }
        },
        error: (error) => {
          this.notification.warning('Warning!!! ', 'No data was saved !');
        },
      });
    }
  }
  //#endregion

  getDetailsInfoById() {
    this.mraStorageService.getMRAInfoById(this.mraId).subscribe({
      next: (res) => {
        if (res) {
          this.isEditMode = true;
          this.mraInfo = res;

          // Patch the agreementTypeId
          this.mraMouForm.patchValue({
            agreementTypeId: this.mraInfo?.agreementType?.id,
            subjectEnglish: this.mraInfo?.subjectEnglish,
            subjectBangla: this.mraInfo?.subjectBangla,
            nameOfOrganizationEnglish: this.mraInfo?.nameOfOrganizationEnglish,
            nameOfOrganizationBangla: this.mraInfo?.nameOfOrganizationBangla,
            introductionEnglish: this.mraInfo?.introductionEnglish,
            introductionBangla: this.mraInfo?.introductionBangla,
            dateOfSignature: this.mraInfo?.dateOfSignature,
            countryId: this.mraInfo?.country?.id,
          });

          // Map attachmentInfo to specific fields
          this.mraInfo?.attachmentInfo?.forEach(
            (attachment: any, index: number) => {
              if (index === 0) {
                this.mraMouForm.patchValue({
                  attachmentTitle1: attachment.attachmentTitle,
                  accessType1: attachment.accessType.id,
                });
              } else if (index === 1) {
                this.mraMouForm.patchValue({
                  attachmentTitle2: attachment.attachmentTitle,
                  accessType2: attachment.accessType.id,
                });
              } else if (index === 2) {
                this.mraMouForm.patchValue({
                  attachmentTitle3: attachment.attachmentTitle,
                  accessType3: attachment.accessType.id,
                });
              } else if (index === 3) {
                this.mraMouForm.patchValue({
                  attachmentTitle4: attachment.attachmentTitle,
                  accessType4: attachment.accessType.id,
                });
              } else if (index === 4) {
                this.mraMouForm.patchValue({
                  attachmentTitle5: attachment.attachmentTitle,
                  accessType5: attachment.accessType.id,
                });
              }
            }
          );

          // Dynamically assign URLs to variables
          this.attachmentUrl1 = this.mraInfo.attachmentInfo[0]?.file || null;
          this.attachmentUrl2 = this.mraInfo.attachmentInfo[1]?.file || null;
          this.attachmentUrl3 = this.mraInfo.attachmentInfo[2]?.file || null;
          this.attachmentUrl4 = this.mraInfo.attachmentInfo[3]?.file || null;
          this.attachmentUrl5 = this.mraInfo.attachmentInfo[4]?.file || null;

          this.attachmentId1 = this.mraInfo.attachmentInfo[0]?.id || null;
          this.attachmentId2 = this.mraInfo.attachmentInfo[1]?.id || null;
          this.attachmentId3 = this.mraInfo.attachmentInfo[2]?.id || null;
          this.attachmentId4 = this.mraInfo.attachmentInfo[3]?.id || null;
          this.attachmentId5 = this.mraInfo.attachmentInfo[4]?.id || null;

          this.fileShowButtonEnableForAttachment1();
          this.fileShowButtonEnableForAttachment2();
          this.fileShowButtonEnableForAttachment3();
          this.fileShowButtonEnableForAttachment4();
          this.fileShowButtonEnableForAttachment5();
        }
      },
      error: (err) => {
        console.error('Error fetching MRA details:', err);
      },
    });
  }

  fileShowButtonEnableForAttachment1(): void {
    if (this.attachmentUrl1) {
      this.isAttachment1Uploaded = true;
      this.fileShowForAttachment1 = true;
    }
  }

  fileShowButtonEnableForAttachment2(): void {
    if (this.attachmentUrl2) {
      this.isAttachment2Uploaded = true;
      this.fileShowForAttachment2 = true;
    }
  }

  fileShowButtonEnableForAttachment3(): void {
    if (this.attachmentUrl3) {
      this.isAttachment3Uploaded = true;
      this.fileShowForAttachment3 = true;
    }
  }

  fileShowButtonEnableForAttachment4(): void {
    if (this.attachmentUrl4) {
      this.isAttachment4Uploaded = true;
      this.fileShowForAttachment4 = true;
    }
  }

  fileShowButtonEnableForAttachment5(): void {
    if (this.attachmentUrl5) {
      this.isAttachment5Uploaded = true;
      this.fileShowForAttachment5 = true;
    }
  }

  // #region onSelectAttachment1
  onSelectAttachment1(event: any): void {
    const files = event.target.files;
    if (!files || files.length === 0) {
      this.notification.error('error', 'No file selected.');
      return;
    }

    const message = this.utilityService.validateInputFile(
      files,
      this.allowedFileExtensions,
      this.maxFormatFileSize
    );
    if (message) {
      this.isAttachment1Uploaded = false;
      this.notification.error('error', message);
      this.myInputVariable1.nativeElement.value = '';
      return;
    }

    const file = files[0];
    const target: DataTransfer = event.target as DataTransfer;
    if (target.files.length !== 1) {
      throw new Error('Cannot use multiple files');
    }

    const reader = new FileReader();
    reader.onload = () => {
      this.attachment1Base64 = reader.result as string;
      this.filePreviewForAttachment1 = true; // Show the preview button
    };
    reader.readAsDataURL(file);

    this.attachmentUrl1 = file;
    this.fileShowForAttachment1 = false;
    if (this.attachmentUrl1) {
      this.mraMouForm.controls.attachment1.setValue(this.attachmentUrl1);
      this.isAttachment1Uploaded = true;
    }
  }
  // #endregion
  //#region onSelectAttachment2
  onSelectAttachment2(event: any): void {
    const files = event.target.files;
    if (!files || files.length === 0) {
      this.notification.error('error', 'No file selected.');
      return;
    }

    const message = this.utilityService.validateInputFile(
      files,
      this.allowedFileExtensions,
      this.maxFormatFileSize
    );
    if (message) {
      this.notification.error('error', message);
      this.myInputVariable2.nativeElement.value = '';
      this.isAttachment2Uploaded = false;
      return;
    }

    const file = files[0];
    const target: DataTransfer = event.target as DataTransfer;
    if (target.files.length !== 1) {
      throw new Error('Cannot use multiple files');
    }

    const reader = new FileReader();
    reader.onload = () => {
      this.attachment2Base64 = reader.result as string;
      this.filePreviewForAttachment2 = true; // Show the preview button
    };
    reader.readAsDataURL(file);
    this.attachmentUrl2 = file;
    this.fileShowForAttachment2 = false;
    if (this.attachmentUrl2) {
      this.mraMouForm.controls.attachment2.setValue(this.attachmentUrl2);
      this.isAttachment2Uploaded = true;
    }
  }
  //#endregion

  //#region onSelectAttachment3
  onSelectAttachment3(event: any): void {
    const files = event.target.files;
    if (!files || files.length === 0) {
      this.notification.error('error', 'No file selected.');
      return;
    }

    const message = this.utilityService.validateInputFile(
      files,
      this.allowedFileExtensions,
      this.maxFormatFileSize
    );
    if (message) {
      this.notification.error('error', message);
      this.myInputVariable3.nativeElement.value = '';
      this.isAttachment3Uploaded = false;
      return;
    }

    const file = files[0];
    const target: DataTransfer = event.target as DataTransfer;
    if (target.files.length !== 1) {
      throw new Error('Cannot use multiple files');
    }

    const reader = new FileReader();
    reader.onload = () => {
      this.attachment3Base64 = reader.result as string;
      this.filePreviewForAttachment3 = true; // Show the preview button
    };
    reader.readAsDataURL(file);
    this.attachmentUrl3 = file;
    this.fileShowForAttachment3 = false;
    if (this.attachmentUrl3) {
      this.mraMouForm.controls.attachment3.setValue(this.attachmentUrl3);
      this.isAttachment3Uploaded = true;
    }
  }
  //#endregion

  //#region onSelectAttachment4
  onSelectAttachment4(event: any): void {
    const files = event.target.files;
    if (!files || files.length === 0) {
      this.notification.error('error', 'No file selected.');
      return;
    }

    const message = this.utilityService.validateInputFile(
      files,
      this.allowedFileExtensions,
      this.maxFormatFileSize
    );
    if (message) {
      this.notification.error('error', message);
      this.myInputVariable4.nativeElement.value = '';
      this.isAttachment4Uploaded = false;
      return;
    }

    const file = files[0];
    const target: DataTransfer = event.target as DataTransfer;
    if (target.files.length !== 1) {
      throw new Error('Cannot use multiple files');
    }

    const reader = new FileReader();
    reader.onload = () => {
      this.attachment4Base64 = reader.result as string;
      this.filePreviewForAttachment4 = true; // Show the preview button
    };
    reader.readAsDataURL(file);

    this.attachmentUrl4 = file;
    this.fileShowForAttachment4 = false;
    if (this.attachmentUrl4) {
      this.mraMouForm.controls.attachment4.setValue(this.attachmentUrl4);
      this.isAttachment4Uploaded = true;
    }
  }
  //#endregion

  onCancelAttachment1(): void {
    this.deleteAttachment1 = false;
    this.filePreviewForAttachment1 = false;
    this.fileShowForAttachment1 = false;
    this.myInputVariable1.nativeElement.value = '';
    if (this.mraMouForm.controls.attachmentTitle1.value) {
      this.mraMouForm.controls.attachmentTitle1.setValue(null);
    }
    if (this.attachmentUrl1 != null) {
      this.attachmentUrl1 = null;
    }
    if (this.mraMouForm.controls.attachment1.value) {
      this.mraMouForm.controls.attachment1.setValue(null);
    }
    this.isAttachment1Uploaded = false;
  }
  onCancelAttachment2(): void {
    this.deleteAttachment2 = false;
    this.filePreviewForAttachment2 = false;
    this.fileShowForAttachment2 = false;
    this.myInputVariable2.nativeElement.value = '';
    if (this.mraMouForm.controls.attachmentTitle2.value) {
      this.mraMouForm.controls.attachmentTitle2.setValue(null);
    }
    if (this.attachmentUrl2 != null) {
      this.attachmentUrl2 = null;
    }
    if (this.mraMouForm.controls.attachment2.value) {
      this.mraMouForm.controls.attachment2.setValue(null);
    }
    this.isAttachment2Uploaded = false;
  }
  onCancelAttachment3(): void {
    this.deleteAttachment3 = false;
    this.filePreviewForAttachment3 = false;
    this.fileShowForAttachment3 = false;
    this.myInputVariable3.nativeElement.value = '';
    if (this.mraMouForm.controls.attachmentTitle3.value) {
      this.mraMouForm.controls.attachmentTitle3.setValue(null);
    }
    if (this.attachmentUrl3 != null) {
      this.attachmentUrl3 = null;
    }
    if (this.mraMouForm.controls.attachment3.value) {
      this.mraMouForm.controls.attachment3.setValue(null);
    }
    this.isAttachment3Uploaded = false;
    return;
  }
  onCancelAttachment4(): void {
    this.deleteAttachment4 = false;
    this.filePreviewForAttachment4 = false;
    this.fileShowForAttachment4 = false;
    this.myInputVariable4.nativeElement.value = '';
    if (this.mraMouForm.controls.attachmentTitle4.value) {
      this.mraMouForm.controls.attachmentTitle4.setValue(null);
    }
    if (this.attachmentUrl4 != null) {
      this.attachmentUrl4 = null;
    }
    if (this.mraMouForm.controls.attachment4.value) {
      this.mraMouForm.controls.attachment4.setValue(null);
    }
    this.isAttachment4Uploaded = false;
    return;
  }
  onCancelAttachment5(): void {
    this.deleteAttachment5 = false;
    this.filePreviewForAttachment5 = false;
    this.fileShowForAttachment5 = false;
    this.myInputVariable5.nativeElement.value = '';
    if (this.mraMouForm.controls.attachmentTitle5.value) {
      this.mraMouForm.controls.attachmentTitle5.setValue(null);
    }
    if (this.attachmentUrl5 != null) {
      this.attachmentUrl5 = null;
    }
    if (this.mraMouForm.controls.attachment5.value) {
      this.mraMouForm.controls.attachment5.setValue(null);
    }
    this.isAttachment5Uploaded = false;
    return;
  }

  onDeleteAttachment1(): void {
    if (this.mraMouForm.controls.attachment1) {
      const attachmentValue1 = this.mraMouForm.controls.attachmentTitle1.value;
      this.mraStorageService
        .deleteAttachment(this.mraId, attachmentValue1)
        .subscribe({
          next: (response: any) => {
            if (response) {
              this.onCancelAttachment1();
              if (response.success === true) {
                this.deleteAttachment1 = true;
                this.notification.warning(
                  'Error!',
                  'Please insert a file for save'
                );
              }
            }
          },
        });
    }
  }
  onDeleteAttachment2(): void {
    if (this.mraMouForm.controls.attachment2) {
      const attachmentValue2 = this.mraMouForm.controls.attachmentTitle2.value;
      this.mraStorageService
        .deleteAttachment(this.mraId, attachmentValue2)
        .subscribe({
          next: (response: any) => {
            if (response) {
              this.onCancelAttachment2();
              if (response.success === true) {
                this.notification.success(
                  'Success !',
                  response.message
                );
              }
            }
          },
        });
    }
  }
  onDeleteAttachment3(): void {
    if (this.mraMouForm.controls.attachment3) {
      const attachmentValue3 = this.mraMouForm.controls.attachmentTitle3.value;
      this.mraStorageService
        .deleteAttachment(this.mraId, attachmentValue3)
        .subscribe({
          next: (response: any) => {
            if (response) {
              this.onCancelAttachment3();
              if (response.success === true) {
                this.notification.success(
                  'Success !',
                  response.message
                );
              }
            }
          },
        });
    }
  }
  onDeleteAttachment4(): void {
    if (this.mraMouForm.controls.attachment4) {
      const attachmentValue4 = this.mraMouForm.controls.attachmentTitle4.value;
      this.mraStorageService
        .deleteAttachment(this.mraId, attachmentValue4)
        .subscribe({
          next: (response: any) => {
            if (response) {
              this.onCancelAttachment4();
              if (response.success === true) {
                this.notification.success(
                  'Success !',
                  response.message
                );
              }
            }
          },
        });
    }
  }
  onDeleteAttachment5(): void {
    if (this.mraMouForm.controls.attachment5) {
      const attachmentValue5 = this.mraMouForm.controls.attachmentTitle5.value;
      this.mraStorageService
        .deleteAttachment(this.mraId, attachmentValue5)
        .subscribe({
          next: (response: any) => {
            if (response) {
              this.onCancelAttachment5();
              if (response.success === true) {
                this.notification.success(
                  'Success !',
                  response.message
                );
              }
            }
          },
        });
    }
  }
  //#region onSelectAttachment5
  onSelectAttachment5(event: any): void {
    const files = event.target.files;
    if (!files || files.length === 0) {
      this.notification.error('error', 'No file selected.');
      return;
    }

    const message = this.utilityService.validateInputFile(
      files,
      this.allowedFileExtensions,
      this.maxFormatFileSize
    );
    if (message) {
      this.notification.error('reror', message);
      this.myInputVariable5.nativeElement.value = '';
      this.isAttachment5Uploaded = false;
      return;
    }

    const file = files[0];
    const target: DataTransfer = event.target as DataTransfer;
    if (target.files.length !== 1) {
      throw new Error('Cannot use multiple files');
    }
    const reader = new FileReader();
    reader.onload = () => {
      this.attachment5Base64 = reader.result as string;
      this.filePreviewForAttachment5 = true; // Show the preview button
    };
    reader.readAsDataURL(file);

    this.attachmentUrl5 = file;
    this.fileShowForAttachment5 = false;
    if (this.attachmentUrl5) {
      this.mraMouForm.controls.attachment5.setValue(this.attachmentUrl5);
      this.isAttachment5Uploaded = true;
    }
  }
  //#endregion

  //#region attachment functionality
  async setBase64AttachmentForPreview(fileName: string) {
    let fileUrl = '';
    switch (fileName) {
      case 'attachment1':
        fileUrl = this.attachmentUrl1 ?? '';
        break;
      case 'attachment2':
        fileUrl = this.attachmentUrl2 ?? '';
        break;
      case 'attachment3':
        fileUrl = this.attachmentUrl3 ?? '';
        break;
      case 'attachment4':
        fileUrl = this.attachmentUrl4 ?? '';
        break;
      case 'attachment5':
        fileUrl = this.attachmentUrl5 ?? '';
        break;
    }
    const data = await fetch(environment.fileServiceApiUrl + fileUrl);
    const blob = await data.blob();
    let fileUrlBase64 = URL.createObjectURL(blob);
    let fileType = this.getFileTypeFromPreviousAttachment(fileUrl);
    this.previewQuestionnaireOrTorImage(fileType, fileUrlBase64);
  }

  previewQuestionnaireOrTorImage(fileType: string | undefined, fileUrl: any) {
    this.imageURL = '';
    this.pdfUrl = '';
    if (fileType == 'image') {
      this.isVisibleForAttachment = true;
      this.imageURL = this.sanitizer.bypassSecurityTrustResourceUrl(fileUrl);
    } else if (fileType == 'pdf') {
      this.isVisibleForAttachment = true;
      this.pdfUrl = this.sanitizer.bypassSecurityTrustResourceUrl(fileUrl);
    } else {
      const link = document.createElement('a');
      link.setAttribute('target', '_blank');
      link.setAttribute('href', fileUrl);
      link.setAttribute('download', 'uploaded_document.' + fileType);
      document.body.appendChild(link);
      link.click();
      link.remove();
    }
  }

  getFileTypeFromPreviousAttachment(fileUrl: string) {
    let contentType = '';
    let basename = fileUrl.split(/[\\/]/).pop();
    let pos = basename?.lastIndexOf('.') ?? 0;

    let fileType = basename?.slice(pos + 1) ?? '';
    if (this.imageTypeArray.includes(fileType)) {
      contentType = 'image';
    } else if (fileType == 'pdf') {
      contentType = 'pdf';
    } else if (fileType == 'doc') {
      contentType = 'doc';
    } else if (fileType == 'docx') {
      contentType = 'docx';
    } else if (fileType == 'xlsx') {
      contentType = 'xlsx';
    } else {
      contentType = 'other';
    }
    return contentType;
  }

  handlePreviewModalCancel(): void {
    this.isVisibleForAttachment = false;
  }

  attachment1Base64: string | null = null;
  attachment2Base64: string | null = null;
  attachment3Base64: string | null = null;
  attachment4Base64: string | null = null;
  attachment5Base64: string | null = null;

  setBase64Attachment1ForPreview(attachment: string): void {
    if (attachment === 'attachment1' && this.attachment1Base64) {
      // Open the file preview in a new tab or modal
      const fileWindow = window.open();
      if (fileWindow) {
        fileWindow.document.write(`
          <iframe src="${this.attachment1Base64}" width="100%" height="100%"></iframe>
        `);
      } else {
        alert(
          'Unable to preview the file. Please check your browser settings.'
        );
      }
    } else {
      alert('No file selected for preview.');
    }
  }
  setBase64Attachment2ForPreview(attachment: string): void {
    if (attachment === 'attachment2' && this.attachment2Base64) {
      // Open the file preview in a new tab or modal
      const fileWindow = window.open();
      if (fileWindow) {
        fileWindow.document.write(`
          <iframe src="${this.attachment2Base64}" width="100%" height="100%"></iframe>
        `);
      } else {
        alert(
          'Unable to preview the file. Please check your browser settings.'
        );
      }
    } else {
      alert('No file selected for preview.');
    }
  }
  setBase64Attachment3ForPreview(attachment: string): void {
    if (attachment === 'attachment3' && this.attachment3Base64) {
      // Open the file preview in a new tab or modal
      const fileWindow = window.open();
      if (fileWindow) {
        fileWindow.document.write(`
          <iframe src="${this.attachment3Base64}" width="100%" height="100%"></iframe>
        `);
      } else {
        alert(
          'Unable to preview the file. Please check your browser settings.'
        );
      }
    } else {
      alert('No file selected for preview.');
    }
  }
  setBase64Attachment4ForPreview(attachment: string): void {
    if (attachment === 'attachment4' && this.attachment4Base64) {
      // Open the file preview in a new tab or modal
      const fileWindow = window.open();
      if (fileWindow) {
        fileWindow.document.write(`
          <iframe src="${this.attachment4Base64}" width="100%" height="100%"></iframe>
        `);
      } else {
        alert(
          'Unable to preview the file. Please check your browser settings.'
        );
      }
    } else {
      alert('No file selected for preview.');
    }
  }

  setBase64Attachment5ForPreview(attachment: string): void {
    if (attachment === 'attachment5' && this.attachment5Base64) {
      // Open the file preview in a new tab or modal
      const fileWindow = window.open();
      if (fileWindow) {
        fileWindow.document.write(`
          <iframe src="${this.attachment5Base64}" width="100%" height="100%"></iframe>
        `);
      } else {
        alert(
          'Unable to preview the file. Please check your browser settings.'
        );
      }
    } else {
      alert('No file selected for preview.');
    }
  }
  filterOption = (input: string, option: any): boolean => {
    return option.nzLabel.toLowerCase().indexOf(input.toLowerCase()) >= 0;
  };
}

 ## 3. **Service  Angular**
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

  getInfoById(
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

 ## 5. ** REST API Spring boot**
    @PostMapping("/save")
    public ResponseEntity<?> saveMRA(@ModelAttribute @Valid MRAResponse mraResponse, BindingResult bindingResult) {
            ApiResponse apiResponse = mraService.saveMra(mraResponse);
            return new ResponseEntity(apiResponse, HttpStatus.OK);
    }

    @PutMapping("/update/{id}")
    public ResponseEntity<?> updateMRA(@PathVariable Long id, @ModelAttribute @Valid MRAResponse mraResponse, BindingResult bindingResult) {
            ApiResponse apiResponse = mraService.updateMra(id, mraResponse);
            return new ResponseEntity(apiResponse, HttpStatus.OK);
    }

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


 ## 7. ** REST DTO Spring boot**

   @Data
public class MRAResponse {
    private Long id;
    private Long agreementTypeId;
    private String subjectEnglish;
    private String subjectBangla;
    private String introductionEnglish;
    private String introductionBangla;
    private String nameOfOrganizationEnglish;
    private String nameOfOrganizationBangla;
    private String dateOfSignature;
    private Long countryId;
    private String attachmentTitle1;
    private Long accessType1;
    private MultipartFile attachment1;
    private Long attachmentId1;
}


 ## 8. **Thank you**