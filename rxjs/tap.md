# tap



## tap

[Documentation](https://rxjs-dev.firebaseapp.com/api/operators/tap)

First encountered this in the [Angular "Tour of Heroes" tutorial](https://angular.io/tutorial) as the first argument of an [Observable](https://rxjs-dev.firebaseapp.com/guide/observable)'s [pipe ](https://rxjs-dev.firebaseapp.com/api/index/function/pipe)method before [catchError](https://rxjs-dev.firebaseapp.com/api/operators/catchError).

{% code-tabs %}
{% code-tabs-item title="hero.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { Observable, of } from 'rxjs';
import { catchError, map, tap } from "rxjs/operators";
import { Hero } from './hero';
import { HEROES } from './mock-heroes';
import { MessageService } from './message.service';
import { HttpClient, HttpHeaders } from "@angular/common/http";

@Injectable({
  providedIn: 'root'
})
export class HeroService {

  private heroesUrl = 'api/heroes';

  constructor(
    private http: HttpClient,
    private messageService: MessageService,
  ) { };

  getHeroes(): Observable<Hero[]>  {
    return this.http.get<Hero[]>(this.heroesUrl)
      .pipe(
        catchError(this.handleError<Hero[]>('getHeroes', []))
      );
  }
  
  getHero(id: number): Observable<Hero> {
    const url = `${this.heroesUrl}/${id}`;
    return this.http.get<Hero>(url).pipe(
      tap(_ => this.log(`fetched hero id=${id}`)),
      catchError(this.handleError<Hero>(`getHero id=${id}`))
    )
  }

  private log(message: string) {
    this.messageService.add(`HeroService: ${message}`);
  }

  private handleError<T> (operation = 'operation', result?: T) {
    return (error: any): Observable<T> => {
      console.log(error);
      this.log(`${operation} failed: ${error.message}}`);
      return of(result as T);
    }
  }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

