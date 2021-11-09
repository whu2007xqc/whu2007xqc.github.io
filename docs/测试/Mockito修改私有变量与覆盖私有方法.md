#### 私有方法
```java
    @Test
    public void partitionTest() {

        Method parition = PowerMockito.method(CommonPartitioner.class, "partition");
        PowerMockito.suppress(parition);

        CommonDetailPartitioner commonDetailPartitioner = new CommonDetailPartitioner();
        commonDetailPartitioner.partition(10);

    }
```


```java
    @Test(expected = ReportException.class)
    public void verifyParamException2Test() throws InvocationTargetException, IllegalAccessException {
        JobParameters jobParameters;
        JobParametersBuilder jobParametersBuilder = new JobParametersBuilder();
        jobParameters = jobParametersBuilder.addString(DATA_DATE,"2021-01-1").toJobParameters();
        Method method = PowerMockito.method(JobExecutionServiceImpl.class, "verifyParam",
                JobExecutionRequestDO.class, JobParameters.class, TaskManagementJobNameMapperEnum.class);
        PowerMockito.when(jobExecutionRequestDO.getRequestId()).thenReturn(1234567l);
        PowerMockito.when(jobExecutionRequestDO.getCurrentJob()).thenReturn(jobDTO);
        PowerMockito.when(jobDTO.getJobName()).thenReturn("jobName");
        method.invoke(jobExecutionService,jobExecutionRequestDO, jobParameters,TaskManagementJobNameMapperEnum.UN_KNOWN_JOB);
    }
```

#### 私有变量
```java
PowerMockito.field(SatAdjustmentMthlyTranSummaryItemReader.class,"itemSwitch").set(satAdjustmentMthlyTranSummaryItemReader, false);
```
set中的satAdjustmentMthlyTranSummaryItemReader为类实例
