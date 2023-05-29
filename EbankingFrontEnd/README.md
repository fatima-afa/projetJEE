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
```typescript
import {HttpClient} from "@angular/common/http";
```
