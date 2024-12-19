---
layout: post
title: Frontend paganation for Country
subtitle: Frontend paganation for country 
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [REST, angular, paganation]
comments: true
mathjax: false
author: Noor
---

# **Paganation frontend Country**  

## 1. **Country Form **  

<div class="card">
  <div class="ng-Header col-xs-12">
    <i nz-icon nzType="form" nzTheme="outline"></i>
    Add Country
  </div>
  <div class="searchboxAerar pt-4">
    <nz-card>
      <form [formGroup]="countryForm" (ngSubmit)="onSubmit()">
        <div class="row justify-content-center media-button mt-4">
          <div class="col-md-5 col-sm-12">
            <nz-form-item>
              <nz-form-label nzRequired>Country Name</nz-form-label>
              <nz-form-control nzErrorTip="Please enter a country name">
                <input
                  nz-input
                  type="text"
                  formControlName="country"
                  id="country"
                  placeholder="Country Name"
                />
              </nz-form-control>
            </nz-form-item>
          </div>
        </div>

        <div class="row justify-content-center media-button mt-4">
          <div class="col-xs-4 col-sm-2">
            <button
              type="submit"
              class="btn btn-success active btn-lg btn-block cari border-redius"
              [disabled]="!countryForm.valid"
            >
              <i nz-icon nzType="save" nzTheme="fill"></i> Submit
            </button>
          </div>
        </div>
      </form>
    </nz-card>
  </div>
## 2. **Paganation frontend Country**  
  <nz-card *ngIf="paginatedCountries.length > 0">
    <div class="ng-Header col-xs-12">
      <i nz-icon nzType="unordered-list" nzTheme="outline"></i>
      {{ "List of Country" | translate }}
    </div>
    <div nz-col [nzSpan]="24">
      <nz-table
        #basicTableOfAttachment
        [nzData]="countries"
        nzTableLayout="fixed"
        nzShowSizeChanger
        nzBordered
        nzSize="middle"
        nzAlign="middle"
        [nzShowTotal]="totalRowRangeTemplateRr"
        [(nzPageSize)]="pageSizeRr"
        [(nzPageIndex)]="currentPageRr"
        [nzShowPagination]="true"
        [nzFrontPagination]="true"
      >
        <ng-template
          #totalRowRangeTemplateRr
          let-range="range"
          let-total
          style="text-align: left"
        >
          Showing {{ range[0] }}-{{ range[1] }} of {{ totalRr }} items
        </ng-template>
        <thead>
          <tr>
            <th style="width: 5%; text-align: center">S/L</th>
            <!-- Serial Number Column -->
            <th style="text-align: center" nzColumnKey="country">Country</th>
            <th style="width: 15%; text-align: center">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let data of basicTableOfAttachment.data; let i = index">
            <!-- Serial Number Column -->
            <td style="text-align: center; vertical-align: middle">
              {{ i + 1 + pageSizeRr * (currentPageRr - 1) }}
            </td>
            <td style="text-align: center; vertical-align: middle">
              {{ data.country }}
            </td>
            <td style="text-align: center">
              <button
                nz-button
                nzType="primary"
                (click)="openEditCountryModal(data)"
                nz-tooltip
                nzTooltipTitle="Edit"
                style="margin: 1%"
              >
                <i nz-icon nzType="edit" nzTheme="outline"></i>
              </button>
              <button
                nz-button
                nzType="danger"
                nz-popconfirm
                nzPopconfirmTitle="Are you sure to delete this item?"
                (nzOnConfirm)="deleteCountry(data.id)"
                style="margin: 1%"
              >
                <i nz-icon nzType="delete" nzTheme="outline"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </nz-table>
    </div>
  </nz-card>
## 1. **Edit Country form**  
  <nz-modal
    [(nzVisible)]="isEditModalVisible"
    nzTitle="Edit Country"
    (nzOnCancel)="isEditModalVisible = false"
  >
    <form [formGroup]="countryForm">
      <label>
        Country Name:
        <input
          type="text"
          placeholder="Country Name"
          formControlName="country"
        />
      </label>
    </form>
  </nz-modal>
</div>

import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { CountryService } from 'src/app/modules/mra/services/country.service';
import { Country } from 'src/app/modules/mra/components/model/country.model';
import { NzNotificationService } from 'ng-zorro-antd/notification';
import { HttpErrorResponse } from '@angular/common/http';
import { applicationPermissions } from 'src/app/shared/application-constants/application-permissions';
import { NzTableQueryParams } from 'ng-zorro-antd/table';

@Component({
  selector: 'app-create-country',
  templateUrl: './create-country.component.html',
  styleUrls: ['./create-country.component.scss'],
})
export class CreateCountryComponent implements OnInit {
  countryForm: FormGroup;
  applicationPermissions = applicationPermissions;
  countries: Country[] = []; // List of countries
  selectedCountry: Country; // Holds the country being edited
  isEditModalVisible: boolean = false;
  isEditMode: boolean = false;
  paginatedCountries: Country[] = []; // The current page of countries to display
  totalRr: number;
  pageSizeRr: number = 10;
  currentPageRr: number = 1;
  sortingKey: string = 'country';
  sortingValue: string = 'descend';

  constructor(
    private fb: FormBuilder,
    private countryService: CountryService,
    private notification: NzNotificationService
  ) {
    this.countryForm = this.fb.group({
      country: [
        '',
        [Validators.required, Validators.pattern(/^(?!\s*$)[a-zA-Z\s]+$/)],
      ],
    });
  }

  ngOnInit(): void {
    this.fetchCountries();
  }

  // Fetch countries with pagination
  fetchCountries(): void {
    const page = this.currentPageRr; // Default to 1 if undefined
    const size = this.pageSizeRr; // Default to 10 if undefined

    // Set the sorting key and sorting value, for example:
    const sortingKey = 'country'; // Sorting by 'name'
    const sortingValue = 'asc'; // Ascending order

    this.countryService.getCountriesAll().subscribe(
      (data) => {
        console.log(data);
        this.countries = data;
        this.updatePaginatedCountries();
      },
      (error) => {
      }
    );
  }

  updatePaginatedCountries(): void {
    const startIndex = (this.currentPageRr - 1) * this.pageSizeRr;
    const endIndex = startIndex + this.pageSizeRr;
    this.paginatedCountries = this.countries.slice(startIndex, endIndex);
  }
  onSubmit(): void {
    if (this.countryForm.valid) {
      const isDuplicate = this.countries.some(
        (country) =>
          country.country.toLowerCase() ===
          this.countryForm.value.country.toLowerCase().trim()
      );

      if (isDuplicate) {
        this.countryForm.controls['country'].setErrors({ duplicate: true });
        this.notification.error('Error', 'Country name already exists !');
        return;
      }

      if (this.isEditMode ) {
        if (!this.selectedCountry?.id) {
          console.warn('Country ID is undefined or invalid; cannot update.');
          return;
        }
        const newCountry: Country = {
          country: this.countryForm.value.country.trim(),
        };
        this.countryService
          .editCountry(this.selectedCountry.id, newCountry)
          .subscribe(
            (response: any) => {
              // Assuming the response has a success indicator
              this.countryForm.reset();
              if (response.success=== false ) {
                this.notification.error(
                  'Fail!',
                  response.message
                );
                return;
              } else if (response.success === true) {
                this.notification.success(
                  'Successful!',
                  response.message
                );
                this.fetchCountries();
                return;
              } else if (response.success === false) {
                this.notification.error(
                  'Fail!',
                  'Country information update Fail!'
                );
                return;
              } else {
                this.notification.error(
                  'Fail!',
                  'Country information update Fail!'
                );
              }
              this.isEditModalVisible = false; // Close the modal
            },
            (error: HttpErrorResponse) => {
              console.error(error);
              this.notification.error(
                'Fail!',
                'Country information update failed!'
              );
            }
          );
      } else {
        const newCountry: Country = {
          country: this.countryForm.value.country.trim(),
        };

        this.countryService.saveCountry(newCountry).subscribe(
          (response: any) => {
            if (response.success === true) {
              this.notification.success(
                'Success!',
                response.message
              );
              this.countryForm.reset();
              this.isEditMode = true; // Reset form
              this.fetchCountries();
            } else if (response.success === false) {
              this.notification.warning('Failed!', 'Country Already Exist!');
              this.countryForm.reset(); // Reset form
            } else {
              this.notification.error(
                'Fail!',
                response.message
              );
            }
          },
          (error) => {
            if (error.status === 400 && error.error && error.error.errors) {
              // Assuming the backend sends validation errors in `error.error.errors`
              for (const field in error.error.errors) {
                if (this.countryForm.controls[field]) {
                  // Set validation errors on specific form controls
                  this.countryForm.controls[field].setErrors({
                    backend: error.error.errors[field],
                  });
                }
              }
              this.notification.error(
                'Validation Failed',
                'Please correct the errors in the form'
              );
            } else {
              this.notification.error(
                'Fail!',
                'Country information save failed'
              );
            }
          }
        );
      }
    }
  }

  deleteCountry(id?: number): void {
    if (id === undefined) {
      this.notification.warning(
        'Warning',
        'Country ID is missing; deletion aborted'
      );
      return;
    }
    this.countryService.deleteCountry(id).subscribe(
      (response: any) => {
        // Update the countries list by removing the deleted country
        this.countries = this.countries.filter((c) => c.id !== id);

        if (response.success === true) {
          this.notification.success(
            'Deleted',
          response.message
          );
          this.fetchCountries();
        } else if (response.success === false) {
          this.notification.error(
            'Failed',
            response.message
          );
        } else {
          this.notification.error(
            'Fail!',
            response.message
          );
        }
      },
      (error) => {
       // Handle specific errors
        if (error.status === 404) {
          this.notification.error(
            'Not Found',
            'The country could not be found or may have already been deleted'
          );
        } else if (error.status === 403) {
          this.notification.error(
            'Unauthorized',
            'You do not have permission to delete this country'
          );
        } else if (error.status === 500) {
          this.notification.error(
            'Server Error',
            'An error occurred on the server. Please try again later.'
          );
        } else {
          this.notification.error(
            'Error',
            'Failed to delete the country. Please try again.'
          );
        }
      }
    );
    this.fetchCountries(); // Refresh the list after deletion
  }

  openEditCountryModal(country: any): void {
    if (!country) {
            return;
    }
    this.selectedCountry = { ...country }; // Clone the object
    this.countryForm.patchValue(this.selectedCountry); // Update form with selected country
    this.isEditModalVisible = false; // Show modal
    this.isEditMode = true;
  }
}

