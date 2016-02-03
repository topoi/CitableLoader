# CitableLoader
The CitableLoader is a Mathematica based tool for downloading JSON files containing resources and metadata
The header is:

`Needs["GeneralUtilities`"];`

`NotebookEvaluate[ 'http://repository.edition-topoi.org/TOOLS/SCIL0001/FlattenHierarchy.nb'];`

### main function (get Citable):

`LoadCitable[input_] := Module[{},Import[input, "JSON"]]`
  
### for data loading
`LoadData[object_] := Module[{},data = ToAssociations@object;
   (Import[URLExecute["http://repository.edition-topoi.org/TOOLS/ReposTOOLS/TOOL0002/ApiSimulator.html"] <> 
        data[["resources"]][[#]][["file"]]]) & /@ 
    Range[Length[data[["resources"]]]]
   ];`

### for metadata loading
`Metadata[object_] := Module[{c}, data = ToAssociations@object;  c = Array[{}, Length[Keys[data[['metadata']]]]]; (c[[#]] = data[['metadata']][[#]] // Dataset) & /@ 
   Range[Length[Keys[data[["metadata"]]]]]]`
