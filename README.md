# DivideAndConquerAlgorithm
분할정복알고리즘(퀵정렬, 합병정렬, 선택문제)

//퀵 정렬
#include <stdio.h>

#define MAX_SIZE 1000

int arr[MAX_SIZE]; // 정렬할 배열
int n; // 배열의 크기

void quick_sort(int left, int right); // 퀵 정렬을 수행하는 함수
int partition(int left, int right); // pivot을 정하는 함수
void swap(int i, int j); // 배열의 두 원소를 교환하는 함수
void read_input(); // 파일에서 정수들을 읽어온 후 배열에 저장하는 함수
void write_output(); // 정렬된 배열을 파일에 출력하는 함수

int main()
{
    read_input(); // 파일에서 입력을 읽어옴
    quick_sort(0, n - 1); // 퀵 정렬 수행
    write_output(); // 정렬된 배열을 출력
    return 0;
}
// 퀵 정렬 함수
void quick_sort(int left, int right)
{
    if (left < right) // 배열 크기가 1보다 큰 경우
    {
        int p = partition(left, right); // pivot을 정하고
        quick_sort(left, p - 1); // 왼쪽 부분배열을 퀵 정렬
        quick_sort(p + 1, right); // 오른쪽 부분배열을 퀵 정렬
    }
}
// pivot을 정하는 함수
int partition(int left, int right)
{
    int pivot = arr[left]; // 첫 번째 원소를 pivot으로 설정
    int i = left + 1; // pivot 다음 위치
    int j = right; // 배열 끝 위치
    while (i <= j) // i와 j가 엇갈리기 전까지 반복
    {
        while (i <= right && arr[i] <= pivot) i++; // pivot보다 큰 원소를 찾음
        while (j >= left + 1 && arr[j] >= pivot) j--; // pivot보다 작은 원소를 찾음
        if (i <= j) swap(i, j); // i와 j를 교환
    }
    swap(left, j); // pivot과 j를 교환
    return j; // pivot 위치 반환
}
// 배열의 두 원소를 교환하는 함수
void swap(int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// 파일에서 정수들을 읽어온 후 배열에 저장하는 함수
void read_input()
{
    FILE* input_file = fopen("data.txt", "r"); // 파일 열기
    if (input_file == NULL) // 파일 열기 실패시
    {
        printf("Failed to open input file.\n");
        return;
    }
    fscanf(input_file, "%d", &n); // 배열의 크기를 읽어옴
    for (int i = 0; i < n; i++)
    {
        fscanf(input_file, "%d", &arr[i]); // 배열의 원소를 읽어옴
    }
    fclose(input_file); // 파일 닫기
}

// 정렬된 배열을 파일에 출력하는 함수
void write_output()
{
    FILE* output_file = fopen("result.txt", "w"); // 파일 열기
    if (output_file == NULL) // 파일 열기 실패시
    {
        printf("Failed to open output file.\n");
        return;
    }
    for (int i = 0; i < n; i++)
    {
        fprintf(output_file, "%d ", arr[i]); // 정렬된 배열을 파일에 출력
    }
    fclose(output_file); // 파일 닫기
}
