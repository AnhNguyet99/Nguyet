# Nguyet
Assignment2
makeCacheMatrix <- function(x = matrix()) { #create a storeable matrix function
    
    InvMatrix <- NULL #store the inverse of the matrix
    
    set <- function(y){ #set the values of the matrix
        
        x <<- y # assign the value y to the variable x
        
        InvMatrix <<-NULL
    }
    
    get <- function() x  # function that gets the value of the matrix 
    
    SetInverse <- function(Matrix_invertion)
    InvMatrix <<- Matrix_invertion
    getInverse <- function() InvMatrix
    #we can get the inverse of the matrix 
    #through the above command

    GetInverse <- function() InvMatrix #get the inverse  matrix
    
    list(set = set,get = get,
         SetInverse = SetInverse,
         GetInverse = GetInverse) # creates the list of data
}

cacheSolve <- function(x, ...) { #function to get the inverse of
    #the matrix from the previous command
    
    InvMatrix<- x$GetInverse ()#check if the inverse function
    #has been calculated or not
    
    if(!is.null(InvMatrix)) { 
        #in the event that the conditions are met, we have
        
        message("Getting cached data")
        return(InvMatrix) 
        #inverse matrix is obtained from the cache
        
    } else { # if not, the calculation will be computed
        
        matrix<-x$get() #get the matrix from object
        InvMatrix<- solve(matrix, ...)
        x$SetInverse(InvMatrix) #set the inverse to the object
        InvMatrix
    }
}

#example
matrix <- makeCacheMatrix(matrix(3:6, 2, 2))
matrix$get()
matrix$GetInverse()
cacheSolve(matrix)
matrix$GetInverse()

