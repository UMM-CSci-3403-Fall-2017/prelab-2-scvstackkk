# Leak report

The leak in check_whitespace.c was caused by the calloc call in the strip subroutine. Because the intermediary pointer value returned by strip, i.e. an arbitrary length non-empty string, must be preserved to evaluate the is_clean function, it cannot be freed. So, a simple if statement in the is_clean function (to seperate the case of the empty string to an actual char*) can be used to simply return false in the empty string case, and otherwise free the pointer value after comparing it to the original string.
