<h1>Digital Banking Front End</h1>
<h3>Installation de Angular</h3>
'ng serve'

<h3>Initialisation du projet :</h3>
'ng new EbankingFrontEnd'

<h3>Models</h3>
<strong>AccountDetails</strong>

```typescript
export interface AccountDetails {
  accountId:            string;
  balance:              number;
  currentPage:          number;
  totalPages:           number;
  pageSize:             number;
  accountOperationDTOS: AccountOperation[];
}
```
<strong>AccountOperation</strong>

```typescript
export interface AccountOperation {
  id:            number;
  operationDate: Date;
  amount:        number;
  type:          string;
  description:   string;
}
```
<strong>Customer</strong>
```typescript
export interface Customer {
  id : number;
  name : string;
  email : string;
}
```

<h3>Services :</h3>
Pour communiquer avec le backend il est evident que l'on aura besoins d'un module http pour le faire :

'import {HttpClient} from "@angular/common/http";'

<H4>Account : </h4>
```typescript
import { Injectable } from '@angular/core';
import {HttpClient} from "@angular/common/http";
import {environment} from "../../environments/environment";
import {Observable} from "rxjs";
import {AccountDetails} from "../model/account.model";

@Injectable({
  providedIn: 'root'
})
export class AccountsService {

  constructor(private http : HttpClient) { }

  public getAccount(accountId : string, page : number, size : number):Observable<AccountDetails>{
    return this.http.get<AccountDetails>(environment.backendHost+"/accounts/"+accountId+"/pageOperations?page="+page+"&size="+size);
  }
  public debit(accountId : string, amount : number, description:string){
    let data={accountId : accountId, amount : amount, description : description}
    return this.http.post(environment.backendHost+"/accounts/debit",data);
  }
  public credit(accountId : string, amount : number, description:string){
    let data={accountId : accountId, amount : amount, description : description}
    return this.http.post(environment.backendHost+"/accounts/credit",data);
  }
  public transfer(accountSource: string,accountDestination: string, amount : number, description:string){
    let data={accountSource, accountDestination, amount, description }
    return this.http.post(environment.backendHost+"/accounts/transfer",data);
  }
}
```
<H4>Customer : </h4>

```typescript
import { Injectable } from '@angular/core';
import {HttpClient} from "@angular/common/http";
import {Observable} from "rxjs";
import {Customer} from "../model/customer.model";
import {environment} from "../../environments/environment";

@Injectable({
  providedIn: 'root'
})
export class CustomerService {
  constructor(private http:HttpClient) { }

  public getCustomers():Observable<Array<Customer>>{
    return this.http.get<Array<Customer>>(environment.backendHost+"/customers")
  }
  public searchCustomers(keyword : string):Observable<Array<Customer>>{
    return this.http.get<Array<Customer>>(environment.backendHost+"/customers/search?keyword="+keyword)
  }
  public saveCustomer(customer: Customer):Observable<Customer>{
    return this.http.post<Customer>(environment.backendHost+"/customers",customer);
  }
  public deleteCustomer(id: number){
    return this.http.delete(environment.backendHost+"/customers/"+id);
  }
}
```
<h3>Réalisation</h3>
<img src="https://s6.imgcdn.dev/rpLHt.png" alt="home page"/>
</br>
<img src="https://s6.imgcdn.dev/rpeIT.png" alt="info Customer page"/>
</br>
<img src="https://s6.imgcdn.dev/rpLHt.png" alt="New customerinfo Customer page"/>
</br>
<img src="https://s6.imgcdn.dev/rpmBD.png" alt="New customer page"/>
</br>
<img src="https://s6.imgcdn.dev/rpqL9.png" alt="account Oper page"/>
</br>
