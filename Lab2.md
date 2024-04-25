---
layout: default
title: Lab2
---
## MiniLab2 - Nonconservative mass transfer



Add a custom stopping Condition for Carbon depletion:



```fortran
integer function extras_finish_step(id)
     integer, intent(in) :: id
     integer :: ierr
     type (star_info), pointer :: s
     ierr = 0
     call star_ptr(id, s, ierr)
     if (ierr /= 0) return
     extras_finish_step = keep_going
     if (s% xa(s% net_iso(ic12),s% nz) < 1d-3 .and. s% xa(s% net_iso(ihe4),s% nz) < 1d-4) then
      extras_finish_step = terminate
      write(*,*) ‘Reached Core Carbon depletion, Model finished evolution.’
     end if
   end function extras_finish_step
```
