# Lab Report 5
```
set -e

rm -rf student-submission
git clone $1 student-submission


cd student-submission

if [ -f ListExamples.java ]
then
    echo "FILE FOUND"
else
    echo "FILE NOT FOUND"
    exit 1
fi

cd ..

cp TestListExamples.java student-submission
cp -r ./lib ./student-submission

cd ./student-submission

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java


if [[ $? -eq 0 ]]
then
  echo "COMPILED"
else
  echo "DID NOT COMPILE"
  exit 1
fi

java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > score.txt

grep -q "2 tests" score.txt
if [[ $? -eq 0 ]]; then
    echo "ALL TESTS PASSES"
fi
grep -q "1 tests" score.txt
if [[ $? -eq 0 ]]; then
    echo "ONE TEST FAILED"
fi
grep -q "0 tests" score.txt
if [[ $? -eq 0 ]]; then
    "ALL TESTS FAILED"
fi   
```

