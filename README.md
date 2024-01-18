# ngx-soap

Simple SOAP client for Angular based on amazing [node-soap](https://github.com/vpulim/node-soap).

Project has been recreated from scratch with Angular CLI.

Please be aware, this package version number will be equal to the corresponding Angular version
0.10.x = v10, 0.11.x = v11, ... 0.16.x = v16

## npm

1. install ngx-soap and dependencies

    `npm install --save ngx-soap-next`

    `npm install --save buffer concat-stream core-js crypto-js events lodash sax stream uuid`

2. Add NgxSoapModule to your app module

    ```
    import { NgxSoapModule } from 'ngx-soap';
    ...
        @NgModule({
            imports: [ ..., NgxSoapModule, ... ]
        ...
    ```
    
3. Inject NgxSoapService in your component:

    ```
    ...
    import { NgxSoapService, Client, ISoapMethodResponse } from 'ngx-soap';
    ...
    
    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {
        client: Client;
        intA = 2;
        intB = 3;
        
        constructor(private soap: NgxSoapService) {
            this.soap.createClient('assets/calculator.wsdl').subscribe(client => this.client = client);
        }
        
        sum() {
            const body = {
              intA: this.intA,
              intB: this.intB
            };
            (<any>this.client).Add(body).subscribe((res: ISoapMethodResponse) => this.message = res.result.AddResult);
        }
    }
    ```

## Local development example

1. `git clone -b angular6-cli-ilb https://github.com/seyfer/ngx-soap.git`
2. `cd ngx-soap && npm install`
3. `ng build ngx-soap`
4. `ng test ngx-soap`
5. `ng serve --proxy-config proxy.conf.json`

See example app under `src/app`

## Author
[Luca Lulani](https://github.com/lula)

## Contributors
[Oleg Abrazhaev](https://github.com/seyfer)
[markward](https://github.com/marcward)
[Andrei Bespamiatnov](https://github.com/AndreyBespamyatnov)
