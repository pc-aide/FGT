# FGT
FGT - Fortigate

````js
document.querySelectorAll('[data-dynamic]').forEach(e=>{
  e.removeAttribute('data-dynamic');
});
````

````js
document.querySelectorAll('script').forEach(s=>{
  if (s.src) s.remove();
});
````
````js
let modal = document.querySelector('.modal-body');
modal.innerHTML = modal.innerHTML;
````
