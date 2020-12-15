  
  DATA:
    ls_edidc  TYPE edi_docnum,
	lt_edidd  TYPE edidd_tt,
	lv_docnum TYPE edi_docnum.
  
  CALL FUNCTION 'EDI_DOCUMENT_OPEN_FOR_READ'
      EXPORTING
        document_number         = iv_docnum "Exist idoc num
      IMPORTING
        idoc_control            = ls_edidc
      EXCEPTIONS
        document_foreign_lock   = 1
        document_not_exist      = 2
        document_number_invalid = 3
        OTHERS                  = 4.
    IF sy-subrc <> 0.
      RETURN.
    ENDIF.

    CALL FUNCTION 'EDI_SEGMENTS_GET_ALL'
      EXPORTING
        document_number         = iv_docnum "Exist idoc num
      TABLES
        idoc_containers         = lt_edidd
      EXCEPTIONS
        document_number_invalid = 1
        end_of_document         = 2
        OTHERS                  = 3.
    IF sy-subrc <> 0.
      RETURN.
    ENDIF.

    CALL FUNCTION 'EDI_DOCUMENT_CLOSE_READ'
      EXPORTING
        document_number   = iv_docnum "Exist idoc num
      EXCEPTIONS
        document_not_open = 1
        parameter_error   = 2
        OTHERS            = 3.
    IF sy-subrc <> 0.
      RETURN.
    ENDIF.
	
   
    "Clear old idoc num. New number will create.
    CLEAR: ls_edidc-docnum.

    CALL FUNCTION 'IDOC_WRITE_AND_START_INBOUND'
      EXPORTING
        i_edidc        = ls_edidc
        do_commit      = abap_true
      IMPORTING
        docnum         = lv_docnum
      TABLES
        i_edidd        = lt_edidd
      EXCEPTIONS
        idoc_not_saved = 1
        OTHERS         = 2.
    IF sy-subrc <> 0.
    ENDIF.	
	
	
	
	
	