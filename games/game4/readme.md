window.uploadedFiles = [];

      function generateUniqueName() {
        const dateTime = Date.now();
        const random5Digit = Math.floor(10000 + Math.random() * 90000);
        return `${dateTime}${random5Digit}`;
      }

            function handleFile(fileType) {
        const splited = fileType.split(".");
        const keyValue = splited[splited.length - 1];
        console.log(keyValue, window.uploadedFiles);
        const findFile = window.uploadedFiles?.find(
          (p) => p?.dataName == keyValue
        );
        if (window.uploadedFiles.length > 0 && findFile) {
          return assetPath + "/" + findFile.fileName;
        } else {
          const splited = fileType.split(".");
          let newData = inputData;
          const joined = splited.map((key) => {
            newData = newData[key];
          });
          return newData;
        }
      }

      function handleValue(valueName) {
        const value = parseInt(document.getElementById(valueName).value);
        if (value) return value;
        else {
          return "";
        }
      }

      function generateJSON() {
        const data = {
          background: handleFile("background"),
          objectImage: handleFile("objectImage"),
          correctObjectImage: handleFile("correctObjectImage"),
          sounds: {
            rotate: handleFile("sounds.rotate"),
            detection: handleFile("sounds.detection"),
            win: handleFile("sounds.win"),
          },
          settings: {
            numObjects: handleValue("numObjects"),
            objectSize: handleValue("objectSize"),
            showDuration: handleValue("showDuration"),
          },
        };

        try {
          window.parent.postMessage(
            {
              type: "saveValues",
              data,
            },
            window.origin
          );
        } catch (error) {
          console.error("Error sending postMessage:", error);
          alert("Failed to send data to parent window.");
        }
      }


      ////////////////////////////////////////////////////////////////
            function handleFile(fileType) {
        const splited = fileType.split(".");
        const keyValue = splited[splited.length - 1];
        // console.log(keyValue, window.uploadedFiles);
        const findFile = window.uploadedFiles?.find(
          (p) => p?.dataName == keyValue
        );
        if (window.uploadedFiles.length > 0 && findFile) {
          return assetPath + "/" + findFile.fileName;
        } else {
          const splited = fileType.split(".");
          let newData = inputData;
          const joined = splited.map((key) => {
            newData = newData[key];
          });
          return newData;
        }
      }

      function handleValue(valueName) {
        const value = parseInt(document.getElementById(valueName).value);
        if (value) return value;
        else {
          return "";
        }
      }

      function generateJSON() {
        const data = {
          background: handleFile("background"),
          objectImage: handleFile("objectImage"),
          correctObjectImage: handleFile("correctObjectImage"),
          sounds: {
            rotate: handleFile("sounds.rotate"),
            detection: handleFile("sounds.detection"),
            win: handleFile("sounds.win"),
          },
          settings: {
            numObjects: handleValue("numObjects"),
            objectSize: handleValue("objectSize"),
            showDuration: handleValue("showDuration"),
          },
        };

        try {
          window.parent.postMessage(
            {
              type: "saveValues",
              inputData: data,
            },
            window.origin
          );
        } catch (error) {
          console.error("Error sending postMessage:", error);
          alert("Failed to send data to parent window.");
        }
      }