# *

- [using di api](#using-di-api)
  - [example code](#code-pieces)
    - [connect to sbo](#connecting)
    - [mess up with document](#document)
    - [mess up with udo](#udo)
  - [run the program](#run-it)
- [fewer example in hana database](#hana-db)
- [helping links](#helping-links)

## using DI API

[SAP B1 DI API installation failed when installing SAP B1 Client](https://answers.sap.com/questions/302160/sap-b1-di-api-installation-failed-when-installing-.html) try `Run as Administrator`

[Is it possible to install DI-API without installing the entire SAP client?](https://answers.sap.com/questions/7125357/is-it-possible-to-install-di-api-without-installin.html) why not just install the client? It is the simplest way to install DI-API. 👍

Can't load xxx.dll / Can't find moniker 👏😁

[When more than 1 Application use the same SAP user, my Application do not connect with DI API.](https://answers.sap.com/questions/196428/error-100000085.html) This is the _License Abuse Prevention_ mechanism in SAP Business One 9.x, and this limitation applies to the DI API also.

### code pieces

[di api error list](https://blogs.sap.com/2017/05/30/sap-di-api-error-list/)

[object types](https://www.ggrenacher.ch/705/sap-business-one-form-types-and-object-types), see also [this one](https://blogs.sap.com/2017/04/27/list-of-object-types/)

how are unique ids sequence numbers generated? [check this](https://stackoverflow.com/questions/5652912/how-are-unique-ids-sequence-numbers-generated-in-sap-b1), but it seems uncompleted

Delivery creation with `Internal error (-5002) occurred`. [If you use `BaseLine` and `BaseEntry`, you need to set the `BaseType` too](https://answers.sap.com/questions/12165504/delivery-creation-with-internal-error--5002-occurr.html)

`-5002` the field should be empty if document is referenced to production order. [Since you are using a base document \(`BaseEntry`, `BaseLine`, `BaseType`\), the `ItemCode` is already defined.](https://answers.sap.com/questions/11369450/issue-for-production-in-di-api.html)

#### connecting

[the Hana instance port number should be added onto the hostname](https://stackoverflow.com/questions/52203464/connect-sap-b1-hana-with-c-sharp-application-using-di-api)

```java
class SBOConnector {
  void test() {
    try {
      company = SBOCOMUtil.newCompany();
      company.setServer("x.x.x.x:port");
      company.setCompanyDB(dbSchema);
      company.setUserName(sbologinUsername);
      company.setPassword(sbologinPassword);
      company.setDbUserName(dbUsername);
      company.setDbPassword(dbPassword);
      company.setDbServerType(SBOCOMConstants.BoDataServerTypes_dst_HANADB);
      // set whether to use trusted connection to db
      company.setUseTrusted(Boolean.FALSE);
      // set SAP Business One language
      company.setLanguage(SBOCOMConstants.BoSuppLangs_ln_Chinese);
      long start = System.currentTimeMillis();
      int connectionResult = company.connect();
      if (connectionResult == 0) {
        log.info("Connected to {}, spent {}ms",
            company.getCompanyName(), System.currentTimeMillis() - start);
      } else {
        throw new SapException(sapErrorMsg(company.getLastError()));
      }
    } catch (Throwable t) {
      throw new SapException(t);
    }
  }
}
```

#### document

[cannot add row without complete selection of batch](https://answers.sap.com/questions/7637415/cannot-add-row-without-complete-selection-of-batch.html), and [why](https://stackoverflow.com/a/62879802) this happens, see also this [example](https://blogs.sap.com/2016/07/13/sample-code-to-update-existing-item-batches-properties-via-di-api/)

```java
class DTest {
  void test() {
    IDocuments doc = SBOCOMUtil.newDocuments(sap.getCompany(), SBOCOMConstants.PMDocumentTypeEnum_pmdt_GoodsIssue);
    doc.getUserFields().getFields().item("Uxx").setValue("xx");
    doc.setComments(source.getComments());
    doc.setTaxDate(source.getTaxDate());
    for (int i = 0; i < 2; i++) {
      doc.getLines().add();
      doc.getLines().setCurrentLine(i);
      doc.getLines().setItemCode(row.getItemCode());
      if (sapReader.isMaterialBatchNoManed("schema", row.getItemCode())) {
        doc.getLines().getBatchNumbers().setBatchNumber(row.getBatch());
        doc.getLines().getBatchNumbers().setQuantity(Double.valueOf(row.getQuantity()));
      }
    }
    if (doc.add() == 0) {
      String newlyGenerateKeyStr = sap.getCompany().GetNewObjectKey();
      log.info(/**/);
    } else {
      log.error(/**/);
    }
  }
}
```

[this example](https://answers.sap.com/questions/13445096/how-to-production-with-di-api.html) used `ICompany#getBusinessObject` to create the bill, but `java.lang.ClassCastException: com.sap.smb.sbo.wrapper.com.Dispatch cannot be cast to x.x.x.x` happens somehow 

[Cannot change `DocDate` or `TaxDate` \(GoodsReceipt\)](https://answers.sap.com/questions/6523583/problame-in-receipt-from-production-in-sap-2007.html)

[get DocNum from a document just created](https://answers.sap.com/questions/456826/docnum-from-a-document-just-created.html)

#### udo

[adding new record in user defined table](https://answers.sap.com/questions/10921803/adding-new-record-in-user-table-via-di-api.html)

[how to pass parameters to `GeneralService`](https://answers.sap.com/questions/54732/jco-sap-b1-how-to-pass-parameters-to-generalservic.html) 👈 the guy on the thread gives some nice explanatory notes

[a transaction already active](https://answers.sap.com/questions/3302255/a-transaction-already-active.html)

[`MasterData` Type UserTable can not add row](https://answers.sap.com/questions/3567176/problem-in-2007-----masterdata-type-usertable-can-.html)

```java
class UTest {
  void test() {
    try {
      ICompanyService companyService = sap.getCompany().getCompanyService();
      sap.getCompany().startTransaction();
      IGeneralService generalService = companyService.getGeneralService("table_name_without_@_symbol");
      Object dispatch = generalService.getDataInterface(SBOCOMConstants.GeneralServiceDataInterfaces_gsGeneralData);
      GeneralData bill = new GeneralData(dispatch);
      bill.setProperty("U_B_Doc_entry", "" + 1);
      bill.setProperty("ass", "");
      // ... other udf
      IGeneralDataParams parma = generalService.add(bill);
      int newlyGeneratedKey = Dispatch.call(param.retrieveRawGeneralDataParams(), "GetProperty", "DocEntry").getInt();
      if (sap.getCompany().isInTransaction()) {
        sap.getCompany().endTransaction(SBOCOMConstants.BoWfTransOpt_wf_Commit);
      }
    } catch (Throwable e) {
      if (sap.getCompany().isInTransaction()) {
        sap.getCompany().endTransaction(SBOCOMConstants.BoWfTransOpt_wf_RollBack);
      }
      loggingService.logError(e, null, fullRequestURL(servletRequest), getClientIP(servletRequest), source.toString());
      return ResponseEntity.ok(SimpleResponse.notOk(sapErrorMsg(sap.getCompany().getLastError())));
    }
  }
}

// If your user defined table has a UDO you can use below method
// https://answers.sap.com/questions/12405412/insert-data-to-user-defined-table.html

// If the UDT is defined as a no Object table you need to use the Usertables object
// , if it's bound to a UDO then you can use general services.
// https://answers.sap.com/questions/10349631/insert-data-in-user-defined-table.html
```

[update user defined table data](https://answers.sap.com/questions/7240525/updating-user-defined-table-master-data-lines-via-.html)

[get auto generated object key from the udo just created](https://answers.sap.com/comments/11850945/view.html)

### run it

If you installed 32bit di api, make sure you run your program with a 32bit jre, e.g., `jre-8u333`

## hana db

`select 13 from dummy`

how to convert `CreateDate` and `CreateTS` to timestamp ? `CreateTS` and `UpdateTS` store just the time in format `hhmmss` as int. That means that `14:34:06` is stored as `143406`. As an int, leading zeros are not stored. [ref](https://stackoverflow.com/questions/53616555/sap-hana-sql-how-to-convert-createts-updatets-crearetime-updatetime-to-timestamp)
```sql
TO_TIMESTAMP(TO_VARCHAR(COALESCE("CreateDate",'19700101'), 'YYYYMMDD') || ' ' || LPAD(COALESCE("CreateTS",0),6,0),'YYYYMMDD HH24MISS')
```

[Pagination query](https://help.sap.com/docs/SAP_ASE/e0d4539d39c34f52ae9ef822c2060077/26d84b4ddae94fed89d4e7c88bc8d1e6.html?version=16.0.4.0&locale=en-US) e.g., `select ... limit 13 offset 31`

[check table's columns information](https://answers.sap.com/answers/10724035/view.html)
```sql
select *
from sys.columns
where schema_name = 'what' and table_name = 'what';
```

## helping links

[\(biuan\) sbo sdk docs](https://biuan.com/)

[\(github\) di api with java example](https://github.com/rafalrozmus/java-and-sap-business-one)

[\(itpub\) 基于SBO java DI接口封装Web服务](http://www.itpub.net/thread-2102133-1-1.html)

[\(csdn\) 通过DI连接SAP实现添加单据功能 \(java\)](https://blog.csdn.net/qq_35844400/article/details/110928817)

[\(cnblog\) SAP常见查询组合](https://www.cnblogs.com/sapSB/p/11969537.html)

[\(sap blogs\) DI API Global Transactions](https://blogs.sap.com/2017/02/03/using-di-api-global-transactions/)
