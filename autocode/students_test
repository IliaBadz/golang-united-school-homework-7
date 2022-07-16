package coverage

import (
	"errors"
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeopleLen(t *testing.T) {

	tests := []struct {
		people People
		wantRes int
	}{
		{people: People{}, wantRes: 0},
		{people: People{Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)}}, wantRes: 1},
		{people: People{
			Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)}, 
			Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)}}, wantRes: 2,},
	}

	for _, tt := range tests {
		t.Run("", func(t *testing.T) {
			result := tt.people.Len()
			if result != tt.wantRes {
				t.Errorf("Expected len to be %d, but got %d", tt.wantRes, result)
			}
		})
	}	
}


func TestPeopleLess(t *testing.T) {
	tests := []struct {
		name string
		people People
		wantRes bool
	}{
		{
			name: "Same names, same birthdays, different surnames", 
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Supe", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},}, 
				wantRes: true,
		},
		{
			name: "Different birthdays", 
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1983, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1981, time.August, 11, 21, 32, 01, 0, time.Local)},},
			wantRes: true,
		},
		{
			name: "Same person",
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
			wantRes: false,
		},
		{
			name: "Different names",
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Homelander", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
			wantRes: true,
		},
		{
			name: "Different surnames, does not need sorting",
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Cutcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
			wantRes: true,
		},
		{
			name: "Different surnames, needs sorting",
			people: People{
				Person{firstName: "Billy", lastName: "Cutcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
			wantRes: false,
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T){
			res := tt.people.Less(0, 1)
			if res != tt.wantRes {
				t.Errorf("Expected output to be %t, but got %t", tt.wantRes, res)
			}
		})
	}
}


func TestSwap(t *testing.T) {

	type positions struct {
		i int
		j int
	}

	tests := []struct {
		name string
		people People
		pos positions
		wantRes People
	}{
		{
			name: "Swap Billy and Homelander", 
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Homelander", lastName: "Supe", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
			pos: positions{i: 0, j: 1},
			wantRes: People{
				Person{firstName: "Homelander", lastName: "Supe", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},},
		},
		{
			name: "Swap Billy and Mon Coeur", 
			people: People{
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1983, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Homelander", lastName: "Supe", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Mon", lastName: "Coeur", birthDay: time.Date(1981, time.August, 11, 21, 32, 01, 0, time.Local)},},
			pos: positions{i: 0, j: 2},
			wantRes: People{
				Person{firstName: "Mon", lastName: "Coeur", birthDay: time.Date(1981, time.August, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Homelander", lastName: "Supe", birthDay: time.Date(1980, time.April, 11, 21, 32, 01, 0, time.Local)},
				Person{firstName: "Billy", lastName: "Butcher", birthDay: time.Date(1983, time.April, 11, 21, 32, 01, 0, time.Local)},},
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.people.Swap(tt.pos.i, tt.pos.j)

			if reflect.DeepEqual(tt.people, tt.wantRes) != true{
				t.Errorf("Expected output to be %+v, but got %+v", tt.wantRes, tt.people)
			}
		})
	}
}

func TestNewMatrix(t *testing.T) {
	tests := []struct {
		name string
		val string
		wantedRes *Matrix
		err error
	}{
		{name: "One row, one column", val: "1", wantedRes: &Matrix{rows: 1, cols: 1, data: []int{1}}, err: nil},
		{name: "One row, two columns", val: "1 2", wantedRes: &Matrix{rows: 1, cols: 2, data: []int{1, 2}}, err: nil},
		{name: "Different row length", val: "1 2\n 3", wantedRes: nil, err: errors.New("Rows need to be the same length")},
		{name: "Two rows, three columns", val: "1 2 3\n 4 5 6", wantedRes: &Matrix{rows: 2, cols: 3, data: []int{1, 2, 3, 4, 5, 6}}, err: nil},
		{name: "Invalid syntax", val: "1 D", wantedRes: nil, err: errors.New("strconv.Atoi: parsing \"D\": invalid syntax")},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T){
			res, err := New(tt.val)
			
			if err != nil && tt.err.Error() != err.Error() {
				t.Errorf("Expected error message to be: %s, but got: %s", tt.err, err)
				return
			}

			if reflect.DeepEqual(res, tt.wantedRes) == false {
				t.Errorf("Expected %+v, but got %+v", tt.wantedRes, res)
			}
		})
	}
}


func TestMatrixRaws(t *testing.T) {
	tests := []struct {
		name string
		val string
		wantedRes [][]int
	}{
		{name: "One row, one element", val: "1", wantedRes: [][]int{{1},}},
		{name: "One row, two elements", val: "1 2", wantedRes: [][]int{{1, 2}}},
		{name: "Two rows, three elements", val: "1 2 3\n 4 5 6", wantedRes: [][]int{{1, 2, 3,}, {4, 5, 6}}},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T){
			res, _ := New(tt.val)
			rows := res.Rows()
			if reflect.DeepEqual(rows, tt.wantedRes) == false {
				t.Errorf("Expected %+v, but got %+v", tt.wantedRes, rows)
			}
		})
	}
}

func TestMatrixColumns(t *testing.T) {
	tests := []struct {
		name string
		val string
		wantedRes [][]int
	}{
		{name: "One column, one element", val: "1", wantedRes: [][]int{{1},}},
		{name: "Two columns", val: "1 2", wantedRes: [][]int{{1}, {2}}},
		{name: "Three columns", val: "1 2 3\n 4 5 6", wantedRes: [][]int{{1, 4}, {2, 5}, {3, 6}}},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T){
			res, _ := New(tt.val)
			cols := res.Cols()
			if reflect.DeepEqual(cols, tt.wantedRes) == false {
				t.Errorf("Expected %+v, but got %+v", tt.wantedRes, cols)
			}
		})
	}
}

func TestMatrixSet(t *testing.T) {
	matrix, _ := New("1 2\n3 4")
	
	tests := []struct {
		name 	string
		row 	int
		col 	int
		val 	int
		wantedRes bool
		resultMatrix *Matrix
	}{
		{name: "Negative row", row: -1, col: 0, val: 11, wantedRes: false, resultMatrix: &Matrix{rows: 2, cols: 2, data: []int{1, 2, 3, 4}}},
		{name: "Negative column", row: 1, col: -1, val: 12, wantedRes: false, resultMatrix: &Matrix{rows: 2, cols: 2, data: []int{1, 2, 3, 4}}},
		{name: "Unexisted row", row: 2, col: 0, val: 13, wantedRes: false, resultMatrix: &Matrix{rows: 2, cols: 2, data: []int{1, 2, 3, 4}}},
		{name: "Unexisted column", row: 1, col: 2, val: 14, wantedRes: false, resultMatrix: &Matrix{rows: 2, cols: 2, data: []int{1, 2, 3, 4}}},
		{name: "Successful", row: 0, col: 1, val: 15, wantedRes: true, resultMatrix: &Matrix{rows: 2, cols: 2, data: []int{1, 15, 3, 4}}},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T){
			res := matrix.Set(tt.row, tt.col, tt.val)
			
			if res != tt.wantedRes {
				t.Errorf("Expected result to be %t, but got %t", tt.wantedRes, res)
				return
			}
			
			if reflect.DeepEqual(tt.resultMatrix, tt.resultMatrix) == false {
				t.Errorf("Expected result to be %+v, but got %+v", tt.resultMatrix, matrix)
			}


		})
	}

}